# Lift parameter names from the callee [10617357] #

**Submitted by Brandon D'Imperio on 11/9/2015 12:00:00 AM**  
**6 votes on UserVoice prior to migration**  

if I have a method with parameters, and close one of the params with another method call, I lose all parameter names unless I copy and paste them:
```
let internal save connection apptId apptPatientId apptPatientInfoId apptProviderScheduledId apptFacilityId apptStartTime apptEndTime apptTypeId apptStatus apptBillingStage apptLoS apptCheckInFlag apptCheckInTime apptCheckOutTime apptForeignEhrId apptAccidentRelated apptAccidentId apptAccidentDate apptAccidentState presentingCondition notesToBiller isChecked apptPrimaryGuarantorType admitStatus (admitFacilityId:int Nullable) referralPcp =
let admitStatus = if String.IsNullOrEmpty(admitStatus) then null else admitStatus
getScalar connection false (fun db -> db.UspAppointmentsInsUpd(apptId, apptPatientId, apptPatientInfoId, apptProviderScheduledId, apptFacilityId, apptStartTime, apptEndTime, apptTypeId, apptStatus, apptBillingStage, apptLoS, apptCheckInFlag, apptCheckInTime, apptCheckOutTime, apptForeignEhrId, apptAccidentRelated, apptAccidentId, apptAccidentDate, apptAccidentState, presentingCondition, notesToBiller, isChecked, apptPrimaryGuarantorType,admitStatus=admitStatus,admitFacilityId=admitFacilityId,referralPcp=referralPcp))
```
then want to close the first parameter with
```
let SaveConn con = save (SqlConn.Conn con)
```
I lose all the remaining parameter names on the tooltip.
Instead I have to do the following
```
let Save apptId apptPatientId apptPatientInfoId apptProviderScheduledId apptFacilityId apptStartTime apptEndTime apptTypeId apptStatus apptBillingStage apptLoS apptCheckInFlag apptCheckInTime apptCheckOutTime apptForeignEhrId apptAccidentRelated apptAccidentId apptAccidentDate apptAccidentState presentingCondition notesToBiller isChecked apptPrimaryGuarantorType admitStatus admitFacilityId referralPcp connString =
save (ConnectionString connString) apptId apptPatientId apptPatientInfoId apptProviderScheduledId apptFacilityId apptStartTime apptEndTime apptTypeId apptStatus apptBillingStage apptLoS apptCheckInFlag apptCheckInTime apptCheckOutTime apptForeignEhrId apptAccidentRelated apptAccidentId apptAccidentDate apptAccidentState presentingCondition notesToBiller isChecked apptPrimaryGuarantorType admitStatus admitFacilityId referralPcp
```
My suggestion is to lift the remaining parameters needed to finish the method call from the callee



## Response ##
** by fslang-admin on 2/4/2016 12:00:00 AM **

Thank you for the suggestion. I have marked it declined per my comment below
Best wishes
Don Syme, F# Core Library and Language Evolution


**[Original UserVoice Submission](https://fslang.uservoice.com/forums/245727-f-language/suggestions/10617357)**


## Comments ##


#### Comment by Sehnsucht on 11/10/2015 7:31:00 PM ####
Aside the current suggestion ; that's a lot of parameter, maybe all those apptXXX args should be in their own type, a record for example (and that way you can "dot into" it and have the field names as a hint when the function is "lifted")


#### Comment by Don Syme on 2/4/2016 4:23:00 PM ####
I don't think we will do this suggestion: the better thing is to redesign an API when there are soooo many parameters, per the comment below.

