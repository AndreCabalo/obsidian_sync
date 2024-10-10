package uol.pagseguro.store.promotion.core.service.impl;  
import lombok.RequiredArgsConstructor;  
import lombok.extern.slf4j.Slf4j;  
import org.springframework.stereotype.Service;  
import uol.pagseguro.store.promotion.core.repository.CategoryRepository;  
import uol.pagseguro.store.promotion.core.repository.MobiPromotionRepository;  
import uol.pagseguro.store.promotion.core.service.CategoryService;  
  
import java.math.BigInteger;  
import java.util.Objects;  
  
@Service  
@Slf4j  
@RequiredArgsConstructor  
public class CategoryServiceImpl implements CategoryService {  
  
    private final MobiPromotionRepository mobiPromotionRepository;  
    private final CategoryRepository categoryRepository;  
  
    private static final BigInteger SPECIAL_CATEGORY_ID = BigInteger.valueOf(1);  
    private static final BigInteger SUBSCRIPTION_PLAN_CATEGORY_ID = BigInteger.valueOf(2);  
  
    @Override  
    public boolean isSpecialPromotion(String promotionName) {  
        boolean isSpecialPromotion = false;  
  
        int idMobiPromotion = mobiPromotionRepository.findIdByName(promotionName);  
        BigInteger categoryIdOfThisPromotion = categoryRepository.findCategoryIdByMobiPromotionId(idMobiPromotion);  
  
        if (Objects.equals(categoryIdOfThisPromotion, SPECIAL_CATEGORY_ID)) {  
            isSpecialPromotion = true;  
        }  
  
        log.info("m=isSpecialPromotion promotionName={}, result={}", promotionName, isSpecialPromotion);  
        return isSpecialPromotion;  
    }  
  
    @Override  
    public boolean isSubscriptionPlanPromotion(String promotionName) {  
        boolean isSubscriptionPlanPromotion = false;  
  
        int idMobiPromotion = mobiPromotionRepository.findIdByName(promotionName);  
        BigInteger categoryIdOfThisPromotion = categoryRepository.findCategoryIdByMobiPromotionId(idMobiPromotion);  
  
        if (Objects.equals(categoryIdOfThisPromotion, SUBSCRIPTION_PLAN_CATEGORY_ID)) {  
            isSubscriptionPlanPromotion = true;  
        }  
  
        log.info("m=isSubscriptionPlanPromotion promotionName={}, result={}", promotionName, isSubscriptionPlanPromotion);  
        return isSubscriptionPlanPromotion;  
    }  
}