package uol.pagseguro.store.promotion.core.service;  
  
public interface CategoryService {  
  
    boolean isSpecialPromotion(String promotionName);  
  
    boolean isSubscriptionPlanPromotion(String promotionName);  
}