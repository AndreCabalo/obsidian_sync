package uol.pagseguro.store.promotion.core.entity;  
  
import lombok.AllArgsConstructor;  
import lombok.NoArgsConstructor;  
import lombok.ToString;  
  
import javax.persistence.*;  
  
import java.math.BigInteger;  
  
import static uol.pagseguro.store.promotion.core.entity.MobiPromotionCategory.ENTITY_NAME;  
import static uol.pagseguro.store.promotion.core.entity.MobiPromotionCategory.TABLE_NAME;  
  
  
@Entity(name = ENTITY_NAME)  
@Table(name = TABLE_NAME)  
@ToString  
@AllArgsConstructor  
@NoArgsConstructor  
public class MobiPromotionCategory {  
  
    static final String ENTITY_NAME = "MobiPromotionCategory";  
    static final String TABLE_NAME = "mobi_promotion_category";  
  
    @Id  
    @Column(name = "IDT_MOBI_PROMOTION")  
    private Integer mobiPromotionId;  
  
    @Id  
    @Column(name = "IDT_CATEGORY")  
    private BigInteger categoryId;  
  
}