package uol.pagseguro.store.promotion.core.entity;  
  
import static uol.pagseguro.store.promotion.core.entity.MobiPromotion.ENTITY_NAME;  
import static uol.pagseguro.store.promotion.core.entity.MobiPromotion.TABLE_NAME;  
  
import java.time.LocalDateTime;  
import java.util.Set;  
  
import javax.persistence.*;  
  
import lombok.AllArgsConstructor;  
import lombok.Builder;  
import lombok.Data;  
import lombok.EqualsAndHashCode;  
import lombok.NoArgsConstructor;  
import lombok.ToString;  
import uol.pagseguro.store.promotion.core.entity.enums.PromotionType;  
  
@Entity(name = ENTITY_NAME)  
@Table(name = TABLE_NAME)  
@Data  
@EqualsAndHashCode(callSuper = true)  
@NoArgsConstructor  
@AllArgsConstructor  
@Builder  
@ToString(callSuper = true)  
public class MobiPromotion extends Auditable {  
  
    static final String ENTITY_NAME = "MobiPromotion";  
    static final String TABLE_NAME = "MOBI_PROMOTION";  
  
    @Id  
    @Column(name = "IDT_MOBI_PROMOTION", nullable = false)  
    private Integer id;  
  
    @Column(name = "NAM_PROMOTION", nullable = false)  
    private String name;  
  
    @Column(name = "DAT_EXPIRATION")  
    private LocalDateTime expirationDate;  
  
    @Column(name = "IND_TYPE", columnDefinition = "CHAR", nullable = false)  
    @Enumerated(EnumType.STRING)  
    private PromotionType promotionType;  
  
    @Column(name = "FLG_REBATE_ENABLE", columnDefinition = "TINYINT(1,0)")  
    private Boolean rebateEnabled;  
  
    @Column(name = "IDT_BC_CONTRACT")  
    private Integer bcContractId;  
  
    @Column(name = "IDT_CARD_READER_PLAN")  
    private Integer cardReaderPlanId;  
  
    @Column(name = "COD_PROMOTION_CODE")  
    private String promotionCode;  
  
    @Column(name = "FLG_ACTIVE", columnDefinition = "TINYINT(1,0)", nullable = false)  
    private Boolean active;  
  
    @ManyToMany(mappedBy = "mobiPromotions")  
    private Set<Category> categories;  
  
}