BEGIN TRAN
INSERT INTO TB_PROD_EQ_ALOC

SELECT  DISTINCT
 'G2011' AS ITM_CD
, ITM_SZ_NM 
,200 AS STL_LENG_A_MIN   ------------------------------
,1600 AS STL_LENG_A_MAX
,200 AS STL_LENG_B_MIN
,1600 AS STL_LENG_B_MAX
,200 AS STL_LENG_C_MIN
,1600 AS STL_LENG_C_MAX   --길이 컬럼
,NULL AS STL_LENG_D_MIN
,NULL AS STL_LENG_D_MAX   
,NULL AS STL_LENG_E_MIN
,NULL AS STL_LENG_E_MAX  ------------------------------
,'2H' AS PROD_EQ_NO      -- 설비 컬럼
,'ROBO' AS CRE_USR_ID  
,CONVERT(DATETIME,2022-06-10) AS CRE_DT
,'ROBO' AS UPD_USR_ID
,GETDATE() AS UPD_DT
,'C210914-ROBO' AS CHNL_CD
FROM TB_CD_ITM           --------------------- TB_CD_ITM에서 조회한 데이터(형상정보) 기준으로 INSERT 
WHERE 1=1
AND CHNL_CD = 'C210914-ROBO'
AND ITM_GRP_CLSS_CD = 'M'          -----------강종 그룹만 조회
AND ITM_CD NOT LIKE '%D1%'          ----------강종 기준으로 INSERT 범위 지정
ORDER BY ITM_SZ_NM

SELECT * FROM TB_PROD_EQ_ALOC

--ROLLBACK TRAN
COMMIT TRAN



----------------------------- 데이터 수정
BEGIN TRAN
UPDATE TB_PROD_EQ_ALOC
   SET 
         --STL_LENG_A_MIN = 0
         --,STL_LENG_A_MAX = 12000
        --,STL_LENG_B_MIN = NULL
       --,STL_LENG_B_MAX = NULL
       --,STL_LENG_C_MIN = NULL
       --,STL_LENG_C_MAX = NULL
       PROD_EQ_NO = 'Cutting'
  WHERE PROD_EQ_ALOC_CD > 195  


----------------------------- 조회 후 커밋

   COMMIT TRAN
