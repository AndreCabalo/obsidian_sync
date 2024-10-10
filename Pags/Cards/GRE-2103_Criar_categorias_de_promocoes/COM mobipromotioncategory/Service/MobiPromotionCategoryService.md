package uol.pagseguro.store.promotion.core.service;  
  
public interface MobiPromotionCategoryService {  
  
    boolean isSpecialPromotion(String promotionName);  
  
    boolean isSubscriptionPlanPromotion(String promotionName);  
}