package uol.pagseguro.store.promotion.core.repository;  
  
import org.springframework.data.jpa.repository.JpaRepository;  
import org.springframework.data.jpa.repository.Query;  
import org.springframework.stereotype.Repository;  
import uol.pagseguro.store.promotion.core.entity.MobiPromotionCategory;  
  
import java.math.BigInteger;  
  
  
@Repository  
public interface MobiPromotionCategoryRepository extends JpaRepository<MobiPromotionCategory, Integer> {  
  
    //TODO posso usar este metodo?  
//    BigInteger findCategoryIdByMobiPromotionId(int mobiPromotionId);  
  
    @Query("SELECT categoryId FROM MobiPromotionCategory WHERE mobiPromotionId = :mobiPromotionId")  
    BigInteger findCategoryIdByMobiPromotionId(int mobiPromotionId);  
  
}