package uol.pagseguro.store.promotion.core.service.impl;  
  
import lombok.extern.slf4j.Slf4j;  
import org.springframework.stereotype.Service;  
import uol.pagseguro.store.promotion.core.repository.MobiPromotionCategoryRepository;  
import uol.pagseguro.store.promotion.core.repository.MobiPromotionRepository;  
import uol.pagseguro.store.promotion.core.service.MobiPromotionCategoryService;  
  
import java.math.BigInteger;  
  
@Service  
@Slf4j  
public class MobiPromotionCategoryServiceImpl implements MobiPromotionCategoryService {  
  
    private MobiPromotionCategoryRepository mobiPromotionCategoryRepository;  
    private MobiPromotionRepository mobiPromotionRepository;  
  
    private static final BigInteger SPECIAL_CATEGORY_ID = BigInteger.valueOf(1);  
    private static final BigInteger SUBSCRIPTION_PLAN_CATEGORY_ID = BigInteger.valueOf(2);  
  
    @Override  
    public boolean isSpecialPromotion(String promotionName) {  
        boolean isSpecialPromotion = false;  
  
        int idMobiPromotion = mobiPromotionRepository.findIdByName(promotionName);  
        BigInteger categoryIdOfThisPromotion = mobiPromotionCategoryRepository.findCategoryIdByMobiPromotionId(idMobiPromotion);  
  
        if (categoryIdOfThisPromotion == SPECIAL_CATEGORY_ID) {  
            isSpecialPromotion = true;  
        }  
  
        log.info("m=isSpecialPromotion promotionName={}, result={}", promotionName, isSpecialPromotion);  
        return isSpecialPromotion;  
    }  
  
    @Override  
    public boolean isSubscriptionPlanPromotion(String promotionName) {  
        boolean isSubscriptionPlanPromotion = false;  
  
        int idMobiPromotion = mobiPromotionRepository.findIdByName(promotionName);  
        BigInteger categoryIdOfThisPromotion = mobiPromotionCategoryRepository.findCategoryIdByMobiPromotionId(idMobiPromotion);  
  
        if (categoryIdOfThisPromotion == SUBSCRIPTION_PLAN_CATEGORY_ID) {  
            isSubscriptionPlanPromotion = true;  
        }  
  
        log.info("m=isSubscriptionPlanPromotion promotionName={}, result={}", promotionName, isSubscriptionPlanPromotion);  
        return isSubscriptionPlanPromotion;  
    }  
}