package uol.pagseguro.store.promotion.core.repository;  
  
import org.springframework.data.jpa.repository.JpaRepository;  
import org.springframework.data.jpa.repository.Query;  
import org.springframework.data.repository.query.Param;  
import org.springframework.stereotype.Repository;  
  
import java.util.List;  
import java.util.Optional;  
  
import uol.pagseguro.store.promotion.core.entity.MobiPromotion;  
import uol.pagseguro.store.promotion.core.entity.vo.MobiPromotionVO;  
  
@Repository  
public interface MobiPromotionRepository extends JpaRepository<MobiPromotion, Integer> {  
  
    @Query("SELECT new uol.pagseguro.store.promotion.core.entity.vo.MobiPromotionVO(mp) "  
            + " FROM MobiPromotion mp "  
            + " WHERE mp.name = :promotionName ")  
    Optional<MobiPromotionVO> findByName(@Param("promotionName") String promotionName);  
  
    @Query("SELECT new uol.pagseguro.store.promotion.core.entity.vo.MobiPromotionVO(mp, mpc, mpcg) "  
            + "FROM MobiPromotionCodeGen mpcg "  
            + "JOIN MobiPromotionCode mpc ON (mpc.id = mpcg.mobiPromotionCodeId) "  
            + "JOIN MobiPromotion mp ON (mp.id = mpc.mobiPromotionId) "  
            + "WHERE mpcg.promotionCodeGen = :promotionCode ")  
    Optional<MobiPromotionVO> findByCode(@Param("promotionCode") String promotionCode);  
  
    @Query("SELECT new uol.pagseguro.store.promotion.core.entity.vo.MobiPromotionVO(mp) "  
            + "FROM MobiPromotionCodeGen mpcg "  
            + "JOIN MobiPromotionCode mpc ON (mpc.id = mpcg.mobiPromotionCodeId) "  
            + "JOIN MobiPromotion mp ON (mp.id = mpc.mobiPromotionId) "  
            + "WHERE mpcg.promotionCodeGen = :promotionCode "  
            + "AND mp.name = :promotionName ")  
    Optional<MobiPromotionVO> findByCodeAndName(@Param("promotionCode") String promotionCode,  
            @Param("promotionName") String promotionName);  
  
    @Query(value = "select COUNT(*) "  
            + " from ("  
            + "    SELECT "  
            + "        mupc.idt_mobi_user_promotion_code "  
            + "    FROM mobi_user_promotion_code as mupc "  
            + "        JOIN mobi_promotion_code_gen as mpcg ON (mpcg.IDT_MOBI_PROMOTION_CODE_GEN = mupc.idt_mobi_promotion_code_gen) "  
            + "        JOIN mobi_user_promotion as mup ON (mup.idt_mobi_user_promotion = mupc.idt_mobi_user_promotion) "  
            + "    WHERE "  
            + "         mup.flg_active = 1 "  
            + "         AND mpcg.COD_PROMOTION_CODE_GEN = :promotionCode "  
            + "    UNION ALL  "  
            + "    SELECT "  
            + "         prc.IDT_PROMOTION_REGISTER_CONTINGENCY "  
            + "    FROM promotion_register_contingency prc "  
            + "        LEFT JOIN promotion_register_contingency prcu ON prc.IDT_PROMOTION_REGISTER_CONTINGENCY = prcu.IDT_PROMOTION_REGISTER_CONTINGENCY_AUTO "  
            + "    WHERE "  
            + "        prc.IND_ACTION_TYPE = 'R' "  
            + "        AND prc.COD_PROMOTION = :promotionCode "  
            + "        AND prc.IND_PROMOTION_CODE_STATUS <> 'S' "  
            + "        AND prc.IND_PROMOTION_STATUS <> 'S' "  
            + "        AND prcu.IDT_PROMOTION_REGISTER_CONTINGENCY IS null "  
            + ") as total ", nativeQuery = true)  
    Long countTotalQuantityOfUsage(@Param("promotionCode") String promotionCode);  
  
    @Query(value = "select COUNT(*) "  
            + " from ("  
            + "    SELECT "  
            + "        mupc.idt_mobi_user_promotion_code "  
            + "    FROM mobi_user_promotion_code as mupc "  
            + "        JOIN mobi_promotion_code_gen as mpcg ON (mpcg.IDT_MOBI_PROMOTION_CODE_GEN = mupc.idt_mobi_promotion_code_gen) "  
            + "        JOIN mobi_user_promotion as mup ON (mup.idt_mobi_user_promotion = mupc.idt_mobi_user_promotion) "  
            + "    WHERE "  
            + "         mup.flg_active = 1 "  
            + "         AND mpcg.COD_PROMOTION_CODE_GEN = :promotionCode "  
            + "         AND mup.idt_safepay_user = :safepayUserId"  
            + "    UNION ALL  "  
            + "    SELECT "  
            + "         prc.IDT_PROMOTION_REGISTER_CONTINGENCY "  
            + "    FROM promotion_register_contingency prc "  
            + "        LEFT JOIN promotion_register_contingency prcu ON prc.IDT_PROMOTION_REGISTER_CONTINGENCY = prcu.IDT_PROMOTION_REGISTER_CONTINGENCY_AUTO \n"  
            + "    WHERE "  
            + "        prc.IND_ACTION_TYPE = 'R' "  
            + "        AND prc.COD_CUSTOMER = :customerCode"  
            + "        AND prc.COD_PROMOTION = :promotionCode "  
            + "        AND prc.IND_PROMOTION_CODE_STATUS <> 'S' "  
            + "        AND prc.IND_PROMOTION_STATUS <> 'S' "  
            + "        AND prcu.IDT_PROMOTION_REGISTER_CONTINGENCY IS null "  
            + ") as total", nativeQuery = true)  
    Long countUserQuantityOfUsage(@Param("safepayUserId") Integer safepayUserId,  
            @Param("promotionCode") String promotionCode, @Param("customerCode") String customerCode);  
  
  
  
    @Query(value = "SELECT idt_mobi_promotion "  
            + "FROM store_promotion.mobi_promotion mp "  
            + "WHERE NAM_PROMOTION = :name ", nativeQuery = true)  
    Integer findIdByName(@Param("name") String name);  
  
//    @Query(value = "select idt_mobi_promotion from store_promotion.mobi_promotion mp where NAM_PROMOTION = :name", nativeQuery = true)  
//    Integer findIdByName(@Param("name") String name);  
  
//TODO posso usar este metodo?  
//    Integer findIdByName(String name);  
  
}