package uol.pagseguro.store.promotion.core.repository;  
  
import org.springframework.data.jpa.repository.JpaRepository;  
import org.springframework.data.jpa.repository.Query;  
import org.springframework.stereotype.Repository;  
import uol.pagseguro.store.promotion.core.entity.Category;  
  
import java.math.BigInteger;  
  
@Repository  
public interface CategoryRepository extends JpaRepository<Category, BigInteger> {  
  
    @Query(value = "SELECT IDT_CATEGORY FROM MOBI_PROMOTION_CATEGORY WHERE IDT_MOBI_PROMOTION = :idMobiPromotion", nativeQuery = true)  
    BigInteger findCategoryIdByMobiPromotionId(int idMobiPromotion);  
}