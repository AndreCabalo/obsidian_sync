package uol.pagseguro.store.promotion.core.entity;  
  
import lombok.AllArgsConstructor;  
import lombok.NoArgsConstructor;  
import lombok.ToString;  
  
import javax.persistence.*;  
  
import java.math.BigInteger;  
import java.util.Set;  
  
import static uol.pagseguro.store.promotion.core.entity.Category.ENTITY_NAME;  
import static uol.pagseguro.store.promotion.core.entity.Category.TABLE_NAME;  
  
@Entity(name = ENTITY_NAME)  
@Table(name = TABLE_NAME)  
@ToString  
@AllArgsConstructor  
@NoArgsConstructor  
public class Category {  
  
    static final String ENTITY_NAME = "Category";  
    static final String TABLE_NAME = "CATEGORY";  
  
    @Id  
    @Column(name = "IDT_CATEGORY")  
    private BigInteger id;  
  
    @Column(name = "NAM_CATEGORY")  
    private String name;  
  
    @ManyToMany  
    @JoinTable(  
            name = "mobi_promotion_category",  
            joinColumns = @JoinColumn(name = "IDT_CATEGORY"),  
            inverseJoinColumns = @JoinColumn(name = "IDT_MOBI_PROMOTION")  
    )  
    private Set<Category> mobiPromotionCategory;  
  
}