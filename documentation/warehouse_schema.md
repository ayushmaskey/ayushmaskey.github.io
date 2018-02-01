create kphcwarehouse
set compatibility level and other settings
add user report with permission db_datareader

need to figure out
kphc-direcotry.dbo.specialist

**create all schema**

| name | use |
|-----|-----|
| kphc_ad |  |
| kphc_all |  |
| kphc_bh |  |
| kphc_cc |  |
| kphc_cps_admin |  |
| kphc_dental |  |
| kphc_doh |  |
| kphc_hchp |  |
| kphc_insurance |  |
| kphc_kaiser |  |
| kphc_kkv |  |
| kphc_opt |  |
| kphc_orders |  |
| kphc_peer |  |
| kphc_pp |  |
| kphc_sara |  |
| kphc_ssis |   |
| kphc_tracking |  |
| kphc_uds |  |
|  |  |
|  |  |

**view **

| name | dependent | use |
|------|-----------|-----|
| kphc_ad.ad_groups_vw |  |  |
| kphc_ad.adComputers_vw |  |  |
| kphc_ad.adusers_vw |  |  |
| kphc_all.controlled_substance_vw |  |  |
| kphc_doh.vwFindCVRPatients |  |  |
| kphc_hchp.vw_CBCM_clients |  |  |
| kphc_insurance.vw_UHC_Medicare_Medicaid_Patient_verified_2017 |  |  |
| kphc_pp.ppAccountsCreated_vw |  |  |
| kphc_sara.abnormalPapMammo_vw |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |


** warehouse tables**

|table| proc_ssis | frequency | data test | description |
|-----|-----------|---------|------|------|
|kphc_ad.ADGroup| kphc_ssis.kphc_ad_ADGroups |  nightly  | good | AD users and groups |
|kphc_ad.ADUSers| kphc_ssis.kphc_ad_ADUSers | nightly | good | AD computers, users and other info |
|kphc_ad.employees| kphc_ssis.kphc_ad_Employees | nightly | good | users, phone, fax etc for website |
|-----|-----------|---------|------|
|kphc_all.Appointments| kphc_ssis.kphc_all_Appointments | nightly | good | all appt since 2014 |
|kphc_all.dimDate| built-in sp | one time | good | date dimension |
|kphc_all.doctorFacility | kphc_ssis.kphcAll_DoctorFacility | nightly | good | all CPS users |
|kphc_all.DocType| kphc_ssis.kphc_all_DocType | nightly | good | Doc Types |
|kphc_all.Document| kphc_ssis.kphc_all_Document | nightly | good | document info |
|kphc_all.Facility|  kphc_ssis.kphc_all_facility  |  nightly | good | all facilities |
|kphc_all.InsuranceCarriers| kphc_ssis.kphc_all_InsuranceCarriers | nightly | good | insurances |
|kphc_all.LogReg| kphc_ssis.kphc_all_LogReg | nightly | good | location of care |
|kphc_all.PatientInsurance| kphc_ssis.kphc_all_PatientInsurance |  nightly | good | patient insrurances |
|kphc_all.PatientProfile| kphc_ssis.kphc_all_PatientProfile | nightly | good | patient profile |
|kphc_all.PatientRace| kphc_ssis.kphc_all_PatientRace | nightly | good | race and subrace |
|kphc_all.PCPChange| kphc_ssis.kphc_all_pcpChange | nightly | good | pcp change |
|-----|-----------|---------|------|
|kphc_bh.BHMetricDetails|    |    |
|kphc_bh.BHMetricDueNow|    |    |
|kphc_bh.BHPatients|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_cc.CCCKD|    |    | nightly | good |
|kphc_cc.CCDiabetes|    |    | nightly | good |
|kphc_cc.CCHabits|    |    | nightly | good |
|kphc_cc.CCHTN|    |    | nightly | good |
|kphc_cc.CCSMG|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_all.Appointment_Activity_Log|    |  | nightly | good |
|kphc_cps_admin.auditData|    |    | nightly | good |
|kphc_cps_admin.CentricityGroups|    |    | nightly | good |
|kphc_cps_admin.CentricityGroupsUsers|    |    | nightly | good |
|kphc_cps_admin.CentricitySecurityDescription| built-in insert | one time |
|kphc_cps_admin.CentricitySecurityGiven|    |    | nightly | good |
|kphc_cps_admin.cpsSecurity | built-in sp | one time | good |
|kphc_cps_admin.quickText|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_dental.slidingFeeCyrca|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_doh.cvrClient|    |    | nightly | good |
|kphc_doh.cvrClientObs|    |    | nightly | good |
|kphc_doh.cvrVisitClinicalList|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_hchp.CBCM_AcuityScore|    |    | nightly | good |
|kphc_hchp.cbcm_metric|    |    | nightly | good |
|kphc_hchp.CBCMMetricDueNow|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_insurance.ER_Vsits|    |    | nightly | good |
|kphc_insurance.ProviderNPI|    |    |
|-----|-----------|---------|------|
|kphc_kaiser.kaiserPatientProfile| built-in insert| one time | good |
|kphc_kaiser.kaiserVisits|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_opt.ContactPrescription|    |    | nightly | good |
|kphc_opt.GlassPrescription|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_orders.EnablingCodes|    |    | nightly | good |
|kphc_orders.OrderCategory|    |    | nightly | good |
|kphc_orders.ReferralCodes|    |    | nightly | good |
|kphc_orders.referralFollowup|    |    | nightly | good |
|kphc_orders.Referrals|    |    | nightly | good |
|kphc_orders.referralSetup|    |    | nightly | good |
|kphc_orders.ReferralSpecialist|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_peer.PeerReviewJune2017|    |    |
|-----|-----------|---------|------|
|kphc_pp.patientPortalSignup|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_sara.breast_diagnosis|    |    | nightly | good |
|kphc_sara.papHPVTracking|    |    | nightly | good |
|-----|-----------|---------|------|
|kphc_uds.CentricityUDS2015|    |    |
|kphc_uds.DentricUDS2015|    |    |
|-----|-----------|---------|------|

**SSIS**

| sp name | dependents | use |
|---------|------------|-----|
| kphc_ssis.kphc_ad_ADGroups | LDAP | users and associated AD groups |
| kphc_ssis.kphc_ad_ADUSers | LDAP | users, computers and associated info |
| kphc_ssis.kphc_ad_Employees | kphc_ssis.kphc_ad_ADUSers | users, phone, fax etc for website |
|  |  |  |
| kphc_ssis.kphc_all_Appointments | cps.appointments, cps.medlist, cps.apptType, kphc_all.patientProfile | all appointments since 2014 |
| kphc_ssis.kphcAll_DoctorFacility | cps.df, cps.usr, cps.medlists, cps.usrgroup, cps.jobTitle, cps. roletype, cps.logreg, cps.specialtytype | all CPS users |
| kphc_ssis.kphc_all_DocType | cps.doctypes | document types with ID |
| kphc_ssis.kphcAll_Document | cps.document, kphc_all.patientProfile  | all documents except file in error and replaced |
| kphc_ssis.kphcAll_facility | cps.doctorfacility | all facilities |
| kphc_ssis.kphc_all_InsuranceCarriers | cps.insuranceCarriers | all carriers |
| kphc_ssis.kphc_all_LogReg | cps.logReg | location of care |
| kphc_ssis.kphc_all_PatientInsurance | kphc_all.patientProfile, cps.patientInsurance | all primary and secondary insurances |
| kphc_ssis.kphc_all_PatientProfile | cps.obs, cps.cusCRIInterview, cps.cusCRIMedLists, cps.cusCustomControlPatientData, cps.cusCustomControlMaster, cps.cusCustomControlDetail, kphc_all.doctorFacility, cps.patientProfile, cps.medLists. cps.patientInsurance, cps.insuranceCarriers, cps.language, kphc_all.patientRace | patient profile |
| kphc_ssis.kphc_all_PatientRace | cps.patientProfile, cps.patientRace, cps.MedLists | patient race |
| kphc_ssis.kphc_all_pcpChange | cps.Obs, kphc_all.patientProfile, kphc_all.doctorFacility | pcp change |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

**Reports**

| sp name | dependents | use |
|---------|------------|-----|
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

**jobs**






