--clear form
declare
	limit_value number;
	total_limit number;
	rate1 number;
	rate2 number;
begin
	begin
		SELECT -- EL.ELEC_PRYM,   --taken as input
					-- EL.ELEC_EMP_PERS_NMBR,-- taken as input;
					 EL.ELEC_HOUS_CODE,
					 EL.ELEC_HOUS_NMBR,
					 EL.ELEC_LAST_READ,
					 EL.ELEC_PRES_READ,
					 EL.ELEC_MTH_NMBR,
					 EL.ELEC_AMT,
					 EM.EMP_FRST_NAME,
					 EM.EMP_CTG_CATG_CODE
		INTO 
		       :WAG_11.HS_TYPE,
		       :WAG_11.HS_NO,
		       :WAG_11.LAST_READ,
		       :WAG_11.PR_READ,
		       :WAG_11.MTH_NO,
		       :WAG_11.ELEC_AMT,
		       :WAG_11.NAME1,
		       :WAG_11.CAT
		FROM 
						ELEC_MSTR EL,EMPL_MSTR EM
		WHERE  EL.ELEC_EMP_PERS_NMBR=:WAG_11.PERS_NO
		AND    EL.ELEC_PRYM=:WAG_11.YYYYMM AND EL.ELEC_EMP_PERS_NMBR=EM.EMP_PERS_NMBR;
	exception when no_data_found then
		message('Invalid Input.Please check.');
	end;
	
	
	:WAG_11.UT_CONS:=:WAG_11.PR_READ-:WAG_11.LAST_READ;--This gives the actual no. of units consumed IN THE NO. OF MONTHS MENTIONED
	:WAG_11.ACT_UNIT:=:WAG_11.UT_CONS;
		
	--Defining the variables
	rate1:=2.40; --for unit below or equal to limit_value
	rate2:=8.77; -- for unit value above the limit_value;
	limit_value:=200;--FOR 1 MONTH
	total_limit:=limit_value*:WAG_11.MTH_NO;	
					
	IF (:WAG_11.UT_CONS<=total_limit)then
		:WAG_11.UT_CONS1:=:WAG_11.UT_CONS;
		:WAG_11.UT_CONS2:=0;
	ELSIF (:WAG_11.UT_CONS>total_limit)then
		:WAG_11.UT_CONS2:=(:WAG_11.UT_CONS-total_limit);
		:WAG_11.UT_CONS1:=total_limit;
	ELSE
		message('Invalid units');
	end if;
	
	
 :WAG_11.BREAK1:=:WAG_11.UT_CONS1*rate1;
 :WAG_11.BREAK2:=:WAG_11.UT_CONS2*rate2;
 :wag_11.total := nvl(:wag_11.break1,0)+nvl(:wag_11.break2,0) ; 
 :WAG_11.RATE1:=rate1;
 :WAG_11.RATE2:=rate2;
end;
previous_item;	
