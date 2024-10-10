package uol.pagseguro.store.promotion.core.service.impl;  
  
import lombok.NonNull;  
import lombok.RequiredArgsConstructor;  
import lombok.extern.slf4j.Slf4j;  
import org.apache.commons.lang3.StringUtils;  
import org.springframework.beans.factory.annotation.Value;  
import org.springframework.stereotype.Service;  
import uol.pagseguro.store.promotion.core.common.AppMetrics;  
import uol.pagseguro.store.promotion.core.dto.PromotionEligibleDTO;  
import uol.pagseguro.store.promotion.core.exception.PromotionEligibilityException;  
import uol.pagseguro.store.promotion.core.exception.PromotionEligibleResponseStatusException;  
import uol.pagseguro.store.promotion.core.service.CategoryService;  
import uol.pagseguro.store.promotion.core.service.EncodeService;  
import uol.pagseguro.store.promotion.core.service.PromotionEligibleService;  
import uol.pagseguro.store.promotion.core.service.strategy.eligibility.MGMPromotionEligibilityStrategy;  
import uol.pagseguro.store.promotion.core.service.strategy.eligibility.SpecialPromotionEligibilityStrategy;  
  
@Slf4j  
@Service  
@RequiredArgsConstructor  
public class PromotionEligibleServiceImpl implements PromotionEligibleService {  
  
    private final CategoryService categoryService;  
    private final AppMetrics appMetrics;  
    private final EncodeService encodeService;  
    private final SpecialPromotionEligibilityStrategy specialPromotionEligibilityStrategy;  
    private final MGMPromotionEligibilityStrategy mgmPromotionEligibilityStrategy;  
  
    @Value("${special-promotion.not-eligible.redirect-url}")  
    private String redirectUrlSpecialPromotion;  
  
    @Override  
    public PromotionEligibleDTO isEligible(@NonNull final String promotionName, @NonNull final String codCustomer, final String mgmCode) {  
        log.info("m=isEligible, promotionName={}, customerCode={}, mgmCode={}", promotionName, codCustomer, mgmCode);  
        try {  
            final boolean isSpecialPromotion = mgmCode == null && categoryService.isSpecialPromotion(promotionName);  
            final boolean isEligible = isEligible(codCustomer, mgmCode, isSpecialPromotion);  
  
            final PromotionEligibleDTO promotionEligibleDTO = PromotionEligibleDTO.builder()  
                    .promotionName(promotionName)  
                    .isSpecialPromotion(isSpecialPromotion)  
                    .isEligible(isEligible)  
                    .redirectUrl(isEligible ? null : buildRedirectUrl(promotionName))  
                    .build();  
  
            if (isSpecialPromotion) {  
                sendCustomEvent(promotionEligibleDTO);  
            }  
  
            log.info("m=isEligible, promotionName={}, codCustomer={}, mgmCode={}, isSpecialPromotion={}, isEligible={}",  
                    promotionName, codCustomer, mgmCode, isSpecialPromotion, promotionEligibleDTO.isEligible());  
            return promotionEligibleDTO;  
  
        } catch (PromotionEligibilityException e) {  
            throw new PromotionEligibleResponseStatusException  
                    (promotionName, codCustomer, e.getMessage(), e.getPayload(), e.getStrategy(), e);  
        }  
    }  
  
    private boolean isEligible(final String codCustomer, final String mgmCode, final boolean isSpecialPromotion) {  
        if (StringUtils.isNotBlank(mgmCode)) {  
            return mgmPromotionEligibilityStrategy.isEligible(codCustomer, mgmCode);  
        }  
        if (isSpecialPromotion) {  
            return specialPromotionEligibilityStrategy.isEligible(codCustomer);  
        }  
        return true;  
    }  
  
    private String buildRedirectUrl(final String promotionName) {  
        return redirectUrlSpecialPromotion + encodeService.encode(promotionName);  
    }  
  
    private void sendCustomEvent(final PromotionEligibleDTO promotionEligible) {  
        try {  
            this.appMetrics.sendCustomEventToInsights(AppMetrics.EVENT_TYPE_SPECIAL_PROMOTION, promotionEligible.getEligiblePromotionEvent());  
        } catch (Exception ex) {  
            log.warn("m=sendCustomEvent, unableToSendSpecialPromotionEvent, message={}", ex.getMessage(), ex);  
        }  
    }  
  
}