---
name: loketnl-api
description: "Loket.nl API skill. Use when working with Loket.nl for providers, automaticpayroll, authorizationmodel. Covers 1087 endpoints."
version: 1.0.0
generator: lapsh
---

# Loket.nl API
API version: V2

## Auth
ApiKey Authorization in header

## Base URL
https://api.loket.nl

## Setup
1. Set your API key in the appropriate header
2. GET /v2/providers/employers/administrations -- verify access
3. POST /v2/providers/employers/employees/{employeeId}/absences -- create first absences

## Endpoints

1087 endpoints across 25 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/providers/employers/employees/{employeeId}/absences | List of absences for an employee |
| POST | /v2/providers/employers/employees/{employeeId}/absences | Create an Absence for an employee |
| GET | /v2/providers/employers/employees/{employeeId}/absences/overview | Download the absence overview for an employee |
| GET | /v2/providers/employers/employees/absences/{absenceId} | Details of an Absence |
| PUT | /v2/providers/employers/employees/absences/{absenceId} | Edit the details of a Absence |
| DELETE | /v2/providers/employers/employees/absences/{absenceId} | Delete a specific absence record |
| PATCH | /v2/providers/employers/employees/absences/{absenceId}/closeabsence | Close an absence |
| PATCH | /v2/providers/employers/employees/absences/{absenceId}/reopenabsence | Reopen an absence |
| GET | /v2/providers/employers/employees/absences/{absenceId}/absenceprogress | List of absence progress for an absence |
| POST | /v2/providers/employers/employees/absences/{absenceId}/absenceprogress | Create an Absence Progress for an Absence |
| GET | /v2/providers/employers/employees/absences/absenceprogress/{absenceProgressId} | Details of an Absence Progress |
| PUT | /v2/providers/employers/employees/absences/absenceprogress/{absenceProgressId} | Edit the details of an absence progress |
| DELETE | /v2/providers/employers/employees/absences/absenceprogress/{absenceProgressId} | Delete a specific Absence Progress record |
| GET | /v2/providers/employers/employees/absences/{absenceId}/absencecontactHistory | Contact history for an absence |
| POST | /v2/providers/employers/employees/absences/{absenceId}/absencecontactHistory | Create a contact history for an Absence |
| GET | /v2/providers/employers/employees/absences/absencecontactHistory/{absencecontactHistoryId} | Details of a contact history |
| PUT | /v2/providers/employers/employees/absences/absencecontactHistory/{absencecontactHistoryId} | Edit the details of a contact history |
| DELETE | /v2/providers/employers/employees/absences/absencecontactHistory/{absencecontactHistoryId} | Delete a specific record |
| GET | /v2/providers/employers/{employerId}/employees/absences/statistics/data | basic absence statistics |
| GET | /v2/providers/employers/{employerId}/administrations | List of administrations for an employer |
| GET | /v2/providers/employers/administrations | List of administrations |
| GET | /v2/providers/employers/{employerId}/payrolladministrations | List of payroll administrations for an employer |
| POST | /v2/providers/employers/{employerId}/payrolladministrations | Add a payroll administration |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId} | Details of a payroll administration |
| GET | /v2/providers/employers/{employerId}/payrolladministrations/configurations | List of payroll administrations configurations for an employer |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/configurations | Details of a payroll administration configuration |
| PUT | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/configurations | Edit a payroll administration configuration |
| GET | /v2/providers/employers/{employerId}/nonpayrolladministrations | List of non payroll administrations for an employer |
| POST | /v2/providers/employers/{employerId}/nonpayrolladministrations | Add a non payroll administration |
| GET | /v2/providers/employers/nonpayrolladministrations/{nonPayrollAdministrationId} | Details of a non payroll administration |
| PUT | /v2/providers/employers/nonpayrolladministrations/{nonPayrollAdministrationId} | Edit a non payroll administration |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/availablepayrollcomponentsets | Available payroll component sets |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollcomponentsets | Payroll component sets |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollcomponentsets | Add an Payroll component set |
| GET | /v2/providers/employers/payrolladministrations/payrollcomponentsets/{payrollComponentSetId} | Details of an payroll component set |
| PUT | /v2/providers/employers/payrolladministrations/payrollcomponentsets/{payrollComponentSetId} | Edit an payroll component set |
| DELETE | /v2/providers/employers/payrolladministrations/payrollcomponentsets/{payrollComponentSetId} | Delete an Payroll component set |
| GET | /v2/providers/{providerId}/payrollcomponentsets | Payroll component sets (provider level) |
| POST | /v2/providers/{providerId}/payrollcomponentsets | Add an Payroll component set (provider level) |
| GET | /v2/providers/payrollcomponentsets/{payrollComponentSetId} | Details of an payroll component set (provider level) |
| PUT | /v2/providers/payrollcomponentsets/{payrollComponentSetId} | Edit an payroll component set (provider level) |
| DELETE | /v2/providers/payrollcomponentsets/{payrollComponentSetId} | Delete an Payroll component set (provider level) |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollcomponents/year/{year} | Payroll components |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/employmentfunds/year/{year} | Employment funds for an administration |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/abpfunds/year/{year} | Abp funds for an administration |
| GET | /v2/providers/employers/{employerId}/employmentActualMasterDataReport | Download actual master data report (Stamgegevens actueel) |
| GET | /v2/providers/employers/{employerId}/employmentMasterDataReport | Download master data report (Stamgegevens) |
| GET | /v2/providers/employers/{employerId}/fiscalCompanyCarReport | Download the fiscal company car report (Auto van de zaak) |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/annualpayrolltaxreturnreport | Download annual payroll tax return report |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/annualwagesheetreport | Download annual wage sheet report |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/annualpawwdeclarationreport | Download annual PAWW declaration report |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrolladministrationsettingsreport | Download payroll administration configuration report |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/accumulationsandbalancesreport | Download accumulations and balances reports |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/accumulatedbasicjournalresultsreport | Download accumulated basic journal results report |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/deviatingpremiumswab | Download WAB deviations report |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/attachmentsofearningsreport | Download attachment of earnings report |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/accumulatedjournalrunresultsreport" | Download accumulated journalrun results report |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollPeriodDataReport | Download annual wage sheet report |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/PayrollAuditReport" | Download payroll audit report |
| GET | /v2/providers/employers/employees/employments/{employmentId}/employmentActualMasterDataReport | Download actual master data report (Stamgegevens actueel) |
| GET | /v2/providers/employers/employees/employments/{employmentId}/employmentMasterDataReport | Download master data report (Stamgegevens) |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollPeriods/{payrollPeriodId}/payrollperioddata | List of payroll period data on payroll administration level |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/import/payrollperioddata" | Import payroll period data for an employer |
| POST | /v2/providers/employers/payrolladministrations/import/payrollperioddata" | Import payroll period data for several employers |
| GET | /v2/providers/employers/{employerId}/workflowtriggers | Get Workflow Triggers by Employer ID |
| GET | /v2/providers/employers/workflowtriggers/workflowtemplates/{workflowTemplateId} | Get Workflow Template |
| PUT | /v2/providers/employers/workflowtriggers/workflowtemplates/{workflowTemplateId} | Edit a workflow template |
| DELETE | /v2/providers/employers/workflowtriggers/workflowtemplates/{workflowTemplateId} | Delete a workflow template |
| POST | /v2/providers/employers/{employerId}/workflowtriggers/{workflowTriggerId}/workflowtemplates | Create a workflow template for a given employer and workflow trigger |
| GET | /v2/providers/employers/{employerId}/workflowtriggermappings | Workflowtrigger to workflowtemplate mapping |
| POST | /v2/providers/employers/{employerId}/workflowtriggermappings | Create a workflow trigger mapping record for an employer |
| GET | /v2/providers/employers/workflowtriggermappings/{workflowTriggerMappingId} | Details of a workflow trigger mapping record |
| PUT | /v2/providers/employers/workflowtriggermappings/{workflowTriggerMappingId} | Edit the details of a workflow trigger mapping record |
| DELETE | /v2/providers/employers/workflowtriggermappings/{workflowTriggerMappingId} | Delete a specific workflow trigger mapping record |
| POST | /v2/providers/employers/employees/{employeeId}/changeaddressrequest | Start the change address workflow for an employee |
| POST | /v2/providers/employers/employees/{employeeId}/changecontactinformationrequest | Start the change contactinformation workflow for an employee |
| POST | /v2/providers/employers/employees/{employeeId}/workflow/InitiateChangeAddress | Initiate the change address workflow for an employee |
| POST | /v2/providers/employers/employees/{employeeId}/workflow/InitiateChangeContactInformation | Initiate the change contact information workflow for an employee |
| POST | /v2/providers/employers/employees/{employeeId}/workflow/InitiateChangePersonalInformation | Initiate the change personal information workflow for an employee |
| POST | /v2/providers/employers/employees/{employeeId}/workflow/InitiateManagePartners | Initiate the change partner information workflow for an employee |
| POST | /v2/providers/employers/employees/{employeeId}/workflow/InitiateManageContacts | Initiate the manage contact workflow for an employee |
| POST | /v2/providers/employers/employees/employments/{employmentId}/workflow/InitiateDeclaration | Initiate the declaration workflow for an employment |
| PATCH | /v2/providers/employers/employees/employments/workflow/{workflowId}/initiatedDeclaration | Change the details of a declaration |
| POST | /v2/providers/employers/employees/employments/{employmentId}/workflow/InitiateChangeIban | Initiate the change IBAN workflow for an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/workflow/InitiateLeaveRequest | Initiate the leave request workflow for an employment |
| PATCH | /v2/providers/employers/employees/employments/workflow/{workflowId}/InitiatedLeaveRequest | Change the details of a leave request |
| POST | /v2/providers/employers/employees/employments/leaveRequests/{leaveRequestId}/workflow/WithdrawLeaveRequest | Initiate the withdraw leave request workflow for a leave request |
| POST | /v2/providers/employers/employees/employments/{employmentId}/workflows/initiatecontractextension | Initiate the contract extension workflow for an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/workflows/initiateterminateemployment | Initiate the employment termination workflow |
| GET | /v2/providers/employers/employees/employments/workflow/{workflowId}/attachment | Download attachment |
| POST | /v2/providers/employers/employees/employments/workflow/{workflowId}/attachment | Upload attachment |
| PATCH | /v2/providers/employers/workflows/{workflowId}/cancel | Cancel a workflow |
| GET | /v2/providers/employers/{employerId}/assignedworkflows | Workflows assigned to the user |
| GET | /v2/providers/employers/{employerId}/workflows | Workflows for the employer |
| GET | /v2/providers/employers/workflows/{workflowId} | Details of a workflow |
| POST | /v2/providers/employers/workflows/{workflowId}/transition | Allows the user to transition the workflow. |
| GET | /v2/providers/employers/employees/employments/{employmentId}/workflows | Workflows for the employment |
| GET | /v2/providers/employers/workflows/{workflowId}/workflowprogress | Progress of a Workflow |
| GET | /v2/providers/employers/{employerId}/employees | List of employees for an employer |
| GET | /v2/providers/employers/employees/{employeeId} | Details of an employee |
| PUT | /v2/providers/employers/employees/{employeeId} | Edit the details of an employee |
| PATCH | /v2/providers/employers/employees/{employeeId} | Change the email address for an employee |
| GET | /v2/providers/employers/employees/{employeeId}/contacts | List of contacts for an employee |
| POST | /v2/providers/employers/employees/{employeeId}/contacts | Create a contact for an employee |
| GET | /v2/providers/employers/employees/contacts/{contactId} | Details of a single contact |
| PUT | /v2/providers/employers/employees/contacts/{contactId} | Edit a contact |
| DELETE | /v2/providers/employers/employees/contacts/{contactId} | Delete a specific contact |
| GET | /v2/providers/employers/employees/{employeeId}/children | List of children for an employee |
| POST | /v2/providers/employers/employees/{employeeId}/children | Create an child for an employee |
| GET | /v2/providers/employers/employees/children/{childId} | Details of a child |
| PUT | /v2/providers/employers/employees/children/{childId} | Edit the details of a child |
| DELETE | /v2/providers/employers/employees/children/{childId} | Delete a specific child record |
| GET | /v2/providers/employers/employees/{employeeId}/occupationaldisabilities | List of occupational disabilities for an employee |
| GET | /v2/providers/employers/employees/{employeeId}/partners | List of partners for an employee |
| POST | /v2/providers/employers/employees/{employeeId}/partners | Create the partner for an employee |
| GET | /v2/providers/employers/employees/partners/{partnerId} | Details of a single partner |
| PUT | /v2/providers/employers/employees/partners/{partnerId} | Edit the details for a partner |
| DELETE | /v2/providers/employers/employees/partners/{partnerId} | Delete a specific partner record |
| GET | /v2/providers/employers/employees/{employeeId}/citizenservicenumber | Citizen service number of an employee |
| PUT | /v2/providers/employers/employees/{employeeId}/citizenservicenumber | Update the citizen service number of an employee |
| GET | /v2/providers/employers/employees/{employeeId}/photo | Photo of an employee |
| POST | /v2/providers/employers/employees/{employeeId}/photo | Post employee photo |
| DELETE | /v2/providers/employers/employees/{employeeId}/photo | Delete employee photo |
| GET | /v2/providers/employers/employees/{employeeId}/photo/{version} | Photo of an employee |
| POST | /v2/providers/employers/{employerId}/employee | Create a new employee in Loket |
| PATCH | /v2/providers/employers/employees/{employeeId}/revokeEmployeeSelfServiceAccess | Set the date on which to revoke ESS access |
| GET | /v2/providers/employers/employees/{employeeId}/customfields | List employee custom fields for an employee |
| POST | /v2/providers/employers/employees/{employeeId}/customfields | Add an employee custom field for an employee |
| GET | /v2/providers/employers/employees/customfields/{employeeCustomFieldId} | Details of an employee custom field |
| PUT | /v2/providers/employers/employees/customfields/{employeeCustomFieldId} | Edit an employee custom field record |
| DELETE | /v2/providers/employers/employees/customfields/{employeeCustomFieldId} | Delete an employee custom field record |
| GET | /v2/providers/employers | List of employers |
| GET | /v2/providers/employers/minimized | List of employers with fewer fields for performance reasons |
| POST | /v2/providers/{providerId}/employers | Create an employer |
| GET | /v2/providers/{providerId}/employers/minimized | List of all employers for the provider |
| GET | /v2/providers/{providerId}/employers/informationForWizard | Determine which steps of the add employer wizard the user can perform |
| GET | /v2/providers/employers/{employerId} | Details of an employer |
| PUT | /v2/providers/employers/{employerId} | Edit the details of an employer |
| GET | /v2/providers/employers/{employerId}/childEmployers | List of child employers accessible to the current user |
| GET | /v2/providers/employers/{employerId}/functions | List of functions |
| POST | /v2/providers/employers/{employerId}/functions | Create a function for an employer |
| GET | /v2/providers/employers/functions/{functionId} | Details of a function |
| PUT | /v2/providers/employers/functions/{functionId} | Edit the details of a function |
| GET | /v2/providers/employers/{employerId}/departments | List of departments |
| POST | /v2/providers/employers/{employerId}/departments | Create a department for an employer |
| GET | /v2/providers/employers/departments/{departmentId} | Details of a department |
| PUT | /v2/providers/employers/departments/{departmentId} | Edit the details of a department |
| GET | /v2/providers/employers/{employerId}/useraccessibledepartments | List of user accessible departments |
| GET | /v2/providers/employers/{employerId}/logo | Logo of an employer |
| DELETE | /v2/providers/employers/{employerId}/logo | Delete the employer logo |
| POST | /v2/providers/employers/{employerId}/logo | Upload a logo for the employer |
| GET | /v2/providers/employers/{employerId}/logo/{version} | Logo of an employer |
| GET | /v2/providers/employers/{employerId}/providerlogo | Provider logo |
| GET | /v2/providers/employers/{employerId}/providerlogo/{version} | Provider logo |
| GET | /v2/providers/employers/{employerId}/dashboard | Dashboard of an employer |
| GET | /v2/providers/employers/{employerId}/customfields | List custom fields for an employer |
| POST | /v2/providers/employers/{employerId}/customfields | Add a custom field for an employer |
| GET | /v2/providers/employers/customfields/{customFieldId} | Details of a custom field |
| PUT | /v2/providers/employers/customfields/{customFieldId} | Edit a custom field record |
| DELETE | /v2/providers/employers/customfields/{customFieldId} | Delete a custom field record |
| GET | /v2/providers/employers/{employerId}/educationtypes | List education types for an employer |
| POST | /v2/providers/employers/{employerId}/educationtypes | Add an education type for an employer |
| GET | /v2/providers/employers/educationtypes/{educationTypeId} | Details of an education type |
| PUT | /v2/providers/employers/educationtypes/{educationTypeId} | Edit an education type record |
| DELETE | /v2/providers/employers/educationtypes/{educationTypeId} | Delete an education type record |
| GET | /v2/providers/employers/{employerId}/educationfurtherindications | List education further indications for an employer |
| POST | /v2/providers/employers/{employerId}/educationfurtherindications | Add an education further indication for an employer |
| GET | /v2/providers/employers/educationfurtherindications/{educationFurtherIndicationId} | Details of an education further indication |
| PUT | /v2/providers/employers/educationfurtherindications/{educationFurtherIndicationId} | Edit an education further indication record |
| DELETE | /v2/providers/employers/educationfurtherindications/{educationFurtherIndicationId} | Delete an education further indication record |
| GET | /v2/providers/employers/{employerId}/contractcodes | List contract codes for an employer |
| POST | /v2/providers/employers/{employerId}/contractcodes | Add a contract code for an employer |
| GET | /v2/providers/employers/contractcodes/{contractCodeId} | Details of a contract code |
| PUT | /v2/providers/employers/contractcodes/{contractCodeId} | Edit a contract code record |
| DELETE | /v2/providers/employers/contractcodes/{contractCodeId} | Delete a contract code record |
| GET | /v2/providers/employers/{employerId}/benefitinkindtypes | List benefit in kind types for an employer |
| POST | /v2/providers/employers/{employerId}/benefitinkindtypes | Add an benefit in kind type for an employer |
| GET | /v2/providers/employers/benefitinkindtypes/{benefitInKindTypeId} | Details of an benefit in kind type |
| PUT | /v2/providers/employers/benefitinkindtypes/{benefitInKindTypeId} | Edit an benefit in kind type record |
| DELETE | /v2/providers/employers/benefitinkindtypes/{benefitInKindTypeId} | Delete an benefit in kind type record |
| GET | /v2/providers/employers/{employerId}/customholidays | List custom holidays for an employer |
| POST | /v2/providers/employers/{employerId}/customholidays | Add a custom holiday for an employer |
| GET | /v2/providers/employers/customholidays/{customHolidayId} | Details of a custom holiday |
| PUT | /v2/providers/employers/customholidays/{customHolidayId} | Edit a custom holiday record |
| DELETE | /v2/providers/employers/customholidays/{customHolidayId} | Delete a custom holiday record |
| GET | /v2/providers/employers/{employerId}/nationalholidays | List of national holidays |
| GET | /v2/providers/employers/{employerId}/nationalholidays/{nationalHolidayId} | Details of a national holiday |
| PUT | /v2/providers/employers/{employerId}/nationalholidays/{nationalHolidayId} | Edit the details of a national holidays |
| GET | /v2/providers/employers/{employerId}/configuration | Employer configuration |
| PUT | /v2/providers/employers/{employerId}/configuration | Edit Employer configuration |
| GET | /v2/providers/employers/{employerId}/distributionunits | List of distribution units |
| POST | /v2/providers/employers/{employerId}/distributionunits | Create a distribution unit for an employer |
| GET | /v2/providers/employers/distributionunits/{distributionUnitId} | Details of a distribution unit |
| PUT | /v2/providers/employers/distributionunits/{distributionUnitId} | Edit the details of a distribution unit |
| GET | /v2/providers/employers/{employerId}/conceptemployees/selfservice | List of Concept employee's and their ESS (WNL) status |
| GET | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/selfservice | Details of a Concept employee self service portal status |
| GET | /v2/providers/employers/{employerId}/employees/selfservice | List of employee's and their ESS (WNL) status |
| PATCH | /v2/providers/employers/{employerId}/employees/selfservice | Change the ESS access for several employees |
| GET | /v2/providers/employers/employees/{employeeId}/selfservice | Details of and employees self service portal status |
| PATCH | /v2/providers/employers/employees/selfservice | Change the employee's self service (ESS) access |
| GET | /v2/providers/employers/{employerId}/employees/selfservice/migration | List of all employees with ESS access (to be migrated to MijnLoket) |
| GET | /v2/providers/employers/{employerId}/employees/essaccessstatus | List of employee's ESS access status |
| PATCH | /v2/providers/employers/{employerId}/employees/essaccessstatus | Change the ESS access for several employees |
| GET | /v2/providers/employers/{employerId}/authorizations | List of authorized activities with regard to the employer |
| GET | /v2/providers/{providerId}/authorizations | List of authorized activities with regard to the provider |
| GET | /v2/providers/employers/{employerId}/modules | List of modules enabled for the employer |
| PATCH | /v2/providers/employers/{employerId}/modules | Enable or disable modules for an employer |
| GET | /v2/providers/{providerId}/modules | List of modules enabled for the provider |
| GET | /v2/providers/employers/{employerId}/conceptemployees | List of concept employee for an employer |
| POST | /v2/providers/employers/{employerId}/conceptemployees | Create a concept employee for an employer |
| GET | /v2/providers/employers/conceptemployees/minimized/{conceptEmployeeId} | Details of a concept employee with fewer fields. |
| PUT | /v2/providers/employers/conceptemployees/minimized/{conceptEmployeeId} | Edit the details of a concept employee with fewer fields. |
| GET | /v2/providers/employers/conceptemployees/{conceptEmployeeId} | Details of a concept employee |
| PUT | /v2/providers/employers/conceptemployees/{conceptEmployeeId} | Edit the details of a concept employee |
| DELETE | /v2/providers/employers/conceptemployees/{conceptEmployeeId} | Delete a concept employee |
| GET | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/citizenservicenumber | Citizen service number of a concept employee |
| PUT | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/citizenservicenumber | Update the citizen service number of a concept employee |
| PATCH | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/convertToEmployee | Convert a concept employee to an employee |
| GET | /v2/providers/employers/conceptemployees/metadata/payrollAdministration/{payrollAdministrationId}/payScale/{payscaleKey}/paygrade/{paygradeKey} | Paygrade metadata for concept employee |
| GET | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/preboardingtrajectory | Get the preboarding trajectory of a concept employee |
| PATCH | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/preboardingtrajectory | Change status of a preboarding trajectory |
| POST | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/preboardingtrajectory | Add a preboarding trajectory |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/employees/employments/actualpaygradeamounts | PayGradeAmounts for the employments |
| POST | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/assessment/initiate | Initiate assessment |
| GET | /v2/providers/employers/{employerId}/assessments | List of assessments |
| GET | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/contactpersons | List of contact persons for a concept employee |
| POST | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/contactpersons | Create a contact person for a concept employee |
| GET | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/contactpersons/metadata | Metadata for contact person creation |
| PUT | /v2/providers/employers/conceptemployees/contactpersons/{contactPersonId} | Edit a contact person |
| DELETE | /v2/providers/employers/conceptemployees/contactpersons/{contactPersonId} | Delete a specific contact person |
| GET | /v2/providers/employers/conceptemployees/contactpersons/{contactPersonId}/metadata | Metadata for contact person update |
| GET | /v2/providers/employers/{employerId}/notifications | Get a list of notifications for an employer. |
| GET | /v2/providers/employers/notifications | Notifications at providerlevel. |
| PATCH | /v2/providers/employers/notifications | Mark one or more notifications as read. |
| GET | /v2/providers/employers/notifications/summary | Number of unread notifications per employer. |
| PATCH | /v2/providers/mutual/employers/notifications | Mark multiple notifications as read. |
| GET | /v2/providers/employers/notifications/{notificationId} | Get notification by ID. |
| GET | /v2/providers/employers/{employerId}/announcements | Get a list of announcements for an employer. |
| GET | /v2/providers/employers/announcements | Announcements at provider level. |
| PATCH | /v2/providers/employers/announcements | Mark one or more announcements as read. |
| GET | /v2/providers/employers/announcements/summary | Unread announcements per employer. |
| PATCH | /v2/providers/mutual/employers/announcements | Mark multiple announcements as read. |
| GET | /v2/providers/employers/announcements/{announcementId} | Details of a single announcement |
| GET | /v2/providers/employers/{employerId}/employees/employments | List of employments for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/minimized | List of employments with fewer fields for performance reasons |
| GET | /v2/providers/employers/{employerId}/employees/employments/comprehensive | List of employments with additional entities |
| GET | /v2/providers/employers/employees/{employeeId}/employments | List of employments for an employee |
| POST | /v2/providers/employers/employees/{employeeId}/employments | Create employment for existing employee |
| GET | /v2/providers/employers/employees/employments/{employmentId} | Details of an employment |
| PUT | /v2/providers/employers/employees/employments/{employmentId} | Edit the details of an employment |
| PATCH | /v2/providers/employers/employees/employments/{employmentId} | Edit the type of an employment |
| DELETE | /v2/providers/employers/employees/employments/{employmentId} | Delete an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/transitioncompensation | Create transition compensation employment for existing employment |
| PATCH | /v2/providers/employers/employees/employments/{employmentId}/employeeprofile | Activate employee profile for the employment |
| GET | /v2/providers/employers/employees/employments/{employmentId}/deleteinformation | Delete employment information |
| PATCH | /v2/providers/employers/employees/employments/{employmentId}/terminate | Terminate an employment. |
| PATCH | /v2/providers/employers/employees/employments/{employmentId}/reinstate | Undo termination for an employment. |
| PATCH | /v2/providers/employers/employees/employments/{employmentId}/correctstartdate | Correct the start (employment) date for an employment. |
| PATCH | /v2/providers/employers/{employerId}/payrollperioddata | Insert or update payroll period data for several employments |
| GET | /v2/providers/employers/employees/employments/{employmentId}/payrollperioddata | list of payroll period data |
| POST | /v2/providers/employers/employees/employments/{employmentId}/payrollperioddata | Create an payroll period data record for an employment |
| PATCH | /v2/providers/employers/employees/employments/{employmentId}/payrollperioddata | Insert or update payroll period data |
| GET | /v2/providers/employers/employees/employments/payrollperioddata/{payrollperioddataId} | Details of a payroll period data |
| PUT | /v2/providers/employers/employees/employments/payrollperioddata/{payrollperioddataId} | Edit the details of an payroll period data |
| DELETE | /v2/providers/employers/employees/employments/payrollperioddata/{payrollperioddataId} | Delete a specific payroll period data record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/benefitsanddeductions | list of benefits and deductions |
| POST | /v2/providers/employers/employees/employments/{employmentId}/benefitsanddeductions | Add a benefit or deduction record for the employment |
| GET | /v2/providers/employers/employees/employments/benefitsAndDeductions/{benefitsanddeductionsId} | Detail of a benefit or deduction record |
| PUT | /v2/providers/employers/employees/employments/benefitsAndDeductions/{benefitsanddeductionsId} | Edit the details of a benefit or deduction record |
| DELETE | /v2/providers/employers/employees/employments/benefitsAndDeductions/{benefitsanddeductionsId} | Delete a specific benefit or deduction record |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/import/benefitsanddeductions" | Get data to create an importfile |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/import/benefitsanddeductions" | Import benefits and deductions via a csv file |
| POST | /v2/providers/employers/{employerId}/employees/employments/benefitsanddeductions | Create benefits and deductions for multiple employments |
| PUT | /v2/providers/employers/{employerId}/employees/employments/benefitsanddeductions | Close benefits and deductions for multiple employments |
| PATCH | /v2/providers/employers/{employerId}/employees/employments/signalpaygradeadjustment | Collective set SignalPayGradeAdjustment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/wageprojection | Perform a wage projection |
| POST | /v2/providers/employers/employees/employments/{employmentId}/wageprojection/basedOnDefaultClaConfiguration | Perform a wage projection based on a default CLA configuration |
| GET | /v2/providers/employers/employees/{employeeId}/educations | List of educations for an employee |
| POST | /v2/providers/employers/employees/{employeeId}/educations | Create a education for an employee |
| GET | /v2/providers/employers/employees/educations/{employeeEducationId} | Details of a single education |
| PUT | /v2/providers/employers/employees/educations/{employeeEducationId} | Edit a Education |
| DELETE | /v2/providers/employers/employees/educations/{employeeEducationId} | Delete a specific education |
| GET | /v2/providers/employers/employees/employments/{employmentId}/declarations | List of declarations for an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/declarations | Create a declaration for an employment |
| GET | /v2/providers/employers/employees/employments/declarations/{declarationId} | Details of a declaration |
| PUT | /v2/providers/employers/employees/employments/declarations/{declarationId} | Edit a declaration for an employment |
| DELETE | /v2/providers/employers/employees/employments/declarations/{declarationId} | Delete a declaration |
| GET | /v2/providers/employers/employees/employments/declarations/{declarationId}/audittrail | Audit trail of a declaration |
| POST | /v2/providers/employers/employees/employments/{employmentId}/declarations/analyze/receipt | Upload a receipt to analyze |
| GET | /v2/providers/employers/employees/employments/{employmentId}/wages | List of wages for an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/wages | Create an wage for an employment |
| GET | /v2/providers/employers/employees/employments/wages/{wageId} | Details of a single wage |
| PUT | /v2/providers/employers/employees/employments/wages/{wageId} | Edit a wage |
| DELETE | /v2/providers/employers/employees/employments/wages/{wageId} | Delete a specific wage record |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/import/wage" | Get data to create an importfile |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/import/wage" | Import wage via a csv file |
| POST | /v2/providers/employers/{employerId}/employees/employments/wages | Create wages for multiple employments |
| GET | /v2/providers/employers/employees/employments/{employmentId}/minimumwage | Minimumwage for an employment |
| GET | /v2/providers/employers/employees/employments/{employmentId}/costperhour | List of costs per hour for an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/costperhour | Add a cost per hour for an employment |
| GET | /v2/providers/employers/employees/employments/costperhour/{costPerHourId} | Details of cost per hour |
| PUT | /v2/providers/employers/employees/employments/costperhour/{costPerHourId} | Edit a cost per hour record |
| DELETE | /v2/providers/employers/employees/employments/costperhour/{costPerHourId} | Delete a cost per hour record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/workinghours | List of working hours for an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/workinghours | Create the working hours for an employment |
| GET | /v2/providers/employers/employees/employments/workinghours/{workinghoursId} | Details of the working hours |
| PUT | /v2/providers/employers/employees/employments/workinghours/{workinghoursId} | Edit the working hours |
| DELETE | /v2/providers/employers/employees/employments/workinghours/{workinghoursId} | Delete a specific working hours record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/organizationalentities | List of organizational entities for an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/organizationalentities | Create an organizational entity for an employment |
| GET | /v2/providers/employers/employees/employments/organizationalentities/{organizationalEntityId} | Details of an organizational entity |
| PUT | /v2/providers/employers/employees/employments/organizationalentities/{organizationalEntityId} | Edit the details of an organizational entity |
| DELETE | /v2/providers/employers/employees/employments/organizationalentities/{organizationalEntityId} | Delete a specific organizational entity record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/paymentinformationsepa | Get a list of payment information sepa |
| POST | /v2/providers/employers/employees/employments/{employmentId}/paymentinformationsepa | create a new payment information sepa record |
| GET | /v2/providers/employers/employees/employments/paymentinformationsepa/{paymentInformationSepaId} | Get the details of a payment information sepa |
| PUT | /v2/providers/employers/employees/employments/paymentinformationsepa/{paymentInformationSepaId} | change the details of a payment information sepa |
| DELETE | /v2/providers/employers/employees/employments/paymentinformationsepa/{paymentInformationSepaId} | Delete a specific SEPA payment-record record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/paymentinformationsepaseparatepayments | Get a list of payment information SEPA separate payment records |
| POST | /v2/providers/employers/employees/employments/{employmentId}/paymentinformationsepaseparatepayments | Create a new payment information SEPA separate payment record |
| GET | /v2/providers/employers/employees/employments/paymentinformationsepaseparatepayments/{paymentInformationSepaSeparatePaymentId} | Get the details of a payment information SEPA separate payment record |
| PUT | /v2/providers/employers/employees/employments/paymentinformationsepaseparatepayments/{paymentInformationSepaSeparatePaymentId} | Edit the details of a payment information separate payment record |
| DELETE | /v2/providers/employers/employees/employments/paymentinformationsepaseparatepayments/{paymentInformationSepaSeparatePaymentId} | Delete a payment information SEPA separate payment record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/paymentinformationnonsepa | Get a list of payment information non-SEPA |
| POST | /v2/providers/employers/employees/employments/{employmentId}/paymentinformationnonsepa | Create a new payment information non-SEPA record |
| GET | /v2/providers/employers/employees/employments/paymentinformationnonsepa/{paymentInformationNonSepaId} | Get the details of a payment information non-SEPA |
| PUT | /v2/providers/employers/employees/employments/paymentinformationnonsepa/{paymentInformationNonSepaId} | Change the details of a payment information non-SEPA |
| DELETE | /v2/providers/employers/employees/employments/paymentinformationnonsepa/{paymentInformationNonSepaId} | Delete a payment information non-SEPA record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/attachmentsofearnings | Get a list of attachment of earnings records |
| POST | /v2/providers/employers/employees/employments/{employmentId}/attachmentsofearnings | Create a new attachment of earnings record |
| GET | /v2/providers/employers/employees/employments/attachmentsofearnings/{attachmentOfEarningsId} | Get the details of an attachment of earnings record |
| PUT | /v2/providers/employers/employees/employments/attachmentsofearnings/{attachmentOfEarningsId} | Edit the details of an attachment of earnings record |
| DELETE | /v2/providers/employers/employees/employments/attachmentsofearnings/{attachmentOfEarningsId} | Delete an attachment of earnings record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/protectedearnings | Get a list of protected earnings records |
| POST | /v2/providers/employers/employees/employments/{employmentId}/protectedearnings | Create a new protected earnings record |
| GET | /v2/providers/employers/employees/employments/protectedearnings/{protectedEarningsId} | Get the details of an protected earnings record |
| PUT | /v2/providers/employers/employees/employments/protectedearnings/{protectedEarningsId} | Edit the details of an protected earnings record |
| DELETE | /v2/providers/employers/employees/employments/protectedearnings/{protectedEarningsId} | Delete an protected earnings record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/fiscalproperties | List of fiscal properties for an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/fiscalproperties | Create a fiscal record for an employment |
| GET | /v2/providers/employers/employees/employments/fiscalproperties/{fiscalPropertiesId} | Details of a fiscal record |
| PUT | /v2/providers/employers/employees/employments/fiscalproperties/{fiscalPropertiesId} | Edit the details of a fiscal record |
| DELETE | /v2/providers/employers/employees/employments/fiscalproperties/{fiscalPropertiesId} | Delete a specific fiscal properties record |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/employees/employments/calculatedannualsalary | Calculate AnnualSalary |
| POST | /v2/providers/employers/{employerId}/employees/employments/fiscalproperties | Create fiscal properties for multiple employments |
| GET | /v2/providers/employers/employees/employments/{employmentId}/fiscalcompanycars | List of fiscal company cars for an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/fiscalcompanycars | Create a fiscal company car record for an employment |
| GET | /v2/providers/employers/employees/employments/fiscalcompanycars/{fiscalCompanyCarId} | Details of a fiscal company car record |
| PUT | /v2/providers/employers/employees/employments/fiscalcompanycars/{fiscalCompanyCarId} | Edit the details of a fiscal company car record |
| DELETE | /v2/providers/employers/employees/employments/fiscalcompanycars/{fiscalCompanyCarId} | Delete a specific fiscal company car record |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/import/fiscalcompanycars | Import fiscal company cars via a csv file |
| GET | /v2/providers/employers/employees/employments/{employmentId}/companycars | List of  company cars for an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/companycars | Create a company car record for an employment |
| GET | /v2/providers/employers/employees/employments/companycars/{companyCarId} | Details of a company car record |
| PUT | /v2/providers/employers/employees/employments/companycars/{companyCarId} | Edit the details of a company car record |
| DELETE | /v2/providers/employers/employees/employments/companycars/{companyCarId} | Delete a specific company car record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/employmentfunds | List of funds the employment partakes in |
| POST | /v2/providers/employers/employees/employments/{employmentId}/employmentfunds | Activate a fund for an employment |
| GET | /v2/providers/employers/employees/employments/employmentfunds/{employmentFundId} | Details of an employment fund |
| PUT | /v2/providers/employers/employees/employments/employmentfunds/{employmentFundId} | Edit a employment fund record |
| DELETE | /v2/providers/employers/employees/employments/employmentfunds/{employmentFundId} | Delete a specific employment fund record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/abpfunds | List of abp funds the employment partakes in |
| POST | /v2/providers/employers/employees/employments/{employmentId}/abpfunds | Activate an abp fund for an employment |
| GET | /v2/providers/employers/employees/employments/abpfunds/{abpFundId} | Details of an abp fund |
| PUT | /v2/providers/employers/employees/employments/abpfunds/{abpFundId} | Edit a abp fund record |
| DELETE | /v2/providers/employers/employees/employments/abpfunds/{abpFundId} | Delete a specific abp fund record |
| POST | /v2/providers/employers/{employerId}/employees/employments/employmentfunds | Create employment funds for multiple employments |
| PATCH | /v2/providers/employers/{employerId}/employees/employments/employmentfunds | Set employment funds enddate for multiple employments |
| POST | /v2/providers/employers/{employerId}/employees/employments/abpfunds | Create abp funds for multiple employments |
| PATCH | /v2/providers/employers/{employerId}/employees/employments/abpfunds | Set abp funds enddate for multiple employments |
| GET | /v2/providers/employers/employees/employments/{employmentId}/basesforemploymentfundcalculation | List of bases for employment fund calculations. |
| POST | /v2/providers/employers/employees/employments/{employmentId}/basesforemploymentfundcalculation | Add a base for employment fund calculation |
| GET | /v2/providers/employers/employees/employments/basesforemploymentfundcalculation/{baseforemploymentfundcalculationId} | Details of an base for employment fund calculations |
| PUT | /v2/providers/employers/employees/employments/basesforemploymentfundcalculation/{baseforemploymentfundcalculationId} | Change the properties of a base for employment fund calculation |
| DELETE | /v2/providers/employers/employees/employments/basesforemploymentfundcalculation/{baseforemploymentfundcalculationId} | Delete a specific record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/basesforcalculation | List of bases for calculations. |
| POST | /v2/providers/employers/employees/employments/{employmentId}/basesforcalculation | Add a base for calculation |
| GET | /v2/providers/employers/employees/employments/basesforcalculation/{baseforcalculationId} | Details of an base for calculation |
| PUT | /v2/providers/employers/employees/employments/basesforcalculation/{baseforcalculationId} | Change the properties of a base for calculation |
| DELETE | /v2/providers/employers/employees/employments/basesforcalculation/{baseforcalculationId} | Delete a specific record |
| POST | /v2/providers/employers/{employerId}/employees/employments/basesforcalculation | Create bases for calculation for multiple employments |
| PATCH | /v2/providers/employers/{employerId}/employees/employments/basesforcalculation | Set base for calculation enddate for multiple employments |
| GET | /v2/providers/employers/employees/employments/{employmentId}/deviatingawfcontributions | List of Deviating AWF contributions records for an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/deviatingawfcontributions | Create a Deviating AWF contributions record for an employment |
| GET | /v2/providers/employers/employees/employments/deviatingawfcontributions/{deviatingAwfContributionId} | Details of a Deviating AWF contributions record |
| PUT | /v2/providers/employers/employees/employments/deviatingawfcontributions/{deviatingAwfContributionId} | Edit the details of a Deviating AWF contributions record |
| DELETE | /v2/providers/employers/employees/employments/deviatingawfcontributions/{deviatingAwfContributionId} | Delete a specific Deviating AWF contributions record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/pensionbenefits | List pension benefit |
| POST | /v2/providers/employers/employees/employments/{employmentId}/pensionbenefits | Add a pension benefit for an employment |
| GET | /v2/providers/employers/employees/employments/pensionbenefits/{pensionBenefitId} | Details of an pension benefit |
| PUT | /v2/providers/employers/employees/employments/pensionbenefits/{pensionBenefitId} | Edit a pension benefit record |
| DELETE | /v2/providers/employers/employees/employments/pensionbenefits/{pensionBenefitId} | Delete a pension benefit record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/deviatinghourlywages | List deviating hourly wage |
| POST | /v2/providers/employers/employees/employments/{employmentId}/deviatinghourlywages | Add a deviating hourly wage for an employment |
| GET | /v2/providers/employers/employees/employments/deviatinghourlywages/{deviatingHourlyWageId} | Details of an deviating hourly wage |
| PUT | /v2/providers/employers/employees/employments/deviatinghourlywages/{deviatingHourlyWageId} | Edit a deviating hourly wage record |
| DELETE | /v2/providers/employers/employees/employments/deviatinghourlywages/{deviatingHourlyWageId} | Delete a deviating hourly wage record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/benefitsInKind | List Benefits in kind |
| POST | /v2/providers/employers/employees/employments/{employmentId}/benefitsInKind | Add a Benefit in kind for an employment |
| GET | /v2/providers/employers/employees/employments/benefitsinkind/{benefitInKindId} | Details of an benefit in kind |
| PUT | /v2/providers/employers/employees/employments/benefitsinkind/{benefitInKindId} | Edit a benefit in kind record |
| DELETE | /v2/providers/employers/employees/employments/benefitsinkind/{benefitInKindId} | Delete a benefit in kind record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/customnotifications | List custom notification |
| POST | /v2/providers/employers/employees/employments/{employmentId}/customnotifications | Add a custom notification for an employment |
| GET | /v2/providers/employers/employees/employments/customnotifications/{customNotificationId} | Details of a custom notification |
| PUT | /v2/providers/employers/employees/employments/customnotifications/{customNotificationId} | Edit a custom notification record |
| DELETE | /v2/providers/employers/employees/employments/customnotifications/{customNotificationId} | Delete a custom notification record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/customfields | List employment custom fields for an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/customfields | Add an employment custom field for an employment |
| GET | /v2/providers/employers/employees/employments/customfields/{employmentCustomFieldId} | Details of an employment custom field |
| PUT | /v2/providers/employers/employees/employments/customfields/{employmentCustomFieldId} | Edit an employment custom field record |
| DELETE | /v2/providers/employers/employees/employments/customfields/{employmentCustomFieldId} | Delete an employment custom field record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/otherPayrollVariables | List of other payroll variables for an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/otherPayrollVariables | Add other payroll variables for an employment |
| GET | /v2/providers/employers/employees/employments/otherPayrollVariables/{otherPayrollVariablesId} | Details of other payroll variables for an employment |
| PUT | /v2/providers/employers/employees/employments/otherPayrollVariables/{otherPayrollVariablesId} | Change the details of an other payroll variables record |
| DELETE | /v2/providers/employers/employees/employments/otherPayrollVariables/{otherPayrollVariablesId} | Delete a specific other payroll variables record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/socialsecurityconfigurations | List of social security records for an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/socialsecurityconfigurations | Create a social security record for an employment |
| GET | /v2/providers/employers/employees/employments/socialsecurityconfigurations/{socialSecurityConfigurationId} | Details of a social security record |
| PUT | /v2/providers/employers/employees/employments/socialsecurityconfigurations/{socialSecurityConfigurationId} | Edit the details of a social security record |
| DELETE | /v2/providers/employers/employees/employments/socialsecurityconfigurations/{socialSecurityConfigurationId} | Delete a specific social security record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/socialsecuritybenefits | List of social security benefits records for an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/socialsecuritybenefits | Create a social security benefits record for an employment |
| GET | /v2/providers/employers/employees/employments/socialsecuritybenefits/{socialSecurityBenefitId} | Details of a social security benefits record |
| PUT | /v2/providers/employers/employees/employments/socialsecuritybenefits/{socialSecurityBenefitId} | Edit the details of a social security benefits record |
| DELETE | /v2/providers/employers/employees/employments/socialsecuritybenefits/{socialSecurityBenefitId} | Delete a specific social security benefits record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/healthcareinsuranceactconfigurations | List of Healthcare Insurance Act records for an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/healthcareinsuranceactconfigurations | Create a Healthcare Insurance Act record for an employment |
| GET | /v2/providers/employers/employees/employments/healthcareinsuranceactconfigurations/{healthcareInsuranceActConfigurationId} | Details of a Healthcare Insurance Act record |
| PUT | /v2/providers/employers/employees/employments/healthcareinsuranceactconfigurations/{healthcareInsuranceActConfigurationId} | Edit the details of a Healthcare Insurance Act record |
| DELETE | /v2/providers/employers/employees/employments/healthcareinsuranceactconfigurations/{healthcareInsuranceActConfigurationId} | Delete a specific Healthcare Insurance Act record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/wachtgeld | List wachtgeld |
| POST | /v2/providers/employers/employees/employments/{employmentId}/wachtgeld | Add a wachtgeld for an employment |
| GET | /v2/providers/employers/employees/employments/wachtgeld/{wachtgeldId} | Details of wachtgeld |
| PUT | /v2/providers/employers/employees/employments/wachtgeld/{wachtgeldId} | Edit a wachtgeld record |
| DELETE | /v2/providers/employers/employees/employments/wachtgeld/{wachtgeldId} | Delete a wachtgeld record |
| GET | /v2/providers/employers/{employerId}/employees/contacts | List of Contacts for an employer |
| GET | /v2/providers/employers/{employerId}/employees/children | List of Children for an employer |
| GET | /v2/providers/employers/{employerId}/employees/citizenservicenumbers | List of citizenServiceNumber for an employer |
| GET | /v2/providers/employers/{employerId}/employees/customfields | List of employee custom fields for an employer |
| GET | /v2/providers/employers/{employerId}/employees/partners | List of Partners for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/customfields | List of employment custom fields for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/paymentinformationsepa | List of payment information for an employer |
| GET | /v2/providers/employers/{employerId}/actualorganizationalentities | List of actual organizational entities for an employer |
| GET | /v2/providers/employers/{employerId}/actualwages | List of actual wages for an employer |
| GET | /v2/providers/employers/{employerId}/actualworkinghours | List of actual working hours for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualbenefitsanddeductions | List of actual benefitsanddeductions for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualemploymentfunds | List of actual employmentfunds for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualabpfunds | List of actual abpfunds for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualfiscalproperties | List of actual fiscal properties for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualhealthcareinsuranceactconfigurations | List of actual healthcare configurations for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualsocialsecurityconfigurations | List of actual social security configurations for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualsocialsecuritybenefits | List of actual social security benefits for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualdeviatingawfcontributions | List of actual awf contributions for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualbenefitsinkind | List of actual benefits in kind for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualcompanycars | List of actual company cars for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualfiscalcompanycars | List of actual fiscal company cars for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualjournalallocations | List of actual journal allocations for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualbasesforcalculation | List of actual bases for calculation for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualotherpayrollvariables | List of actual other payrollvariables for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualpaymentinformationnonsepa | List of actual payment information non sepa for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualbasesforemploymentfundcalculation | List of actual bases for employment fund calculation for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualpensionbenefits | List of actual pension benefits for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualdeviatinghourlywages | List of actual deviating hourly wage for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/actualcostperhour | List of actual cost per hour for an employer |
| GET | /v2/providers/employers/employees/{employeeId}/benifyurl | Get Benify URL for an employee |
| GET | /v2/providers/employers/{employerId}/leavePolicies | List of all the leave policies |
| POST | /v2/providers/employers/{employerId}/leavePolicies | Create a leave policy |
| PATCH | /v2/providers/employers/{employerId}/leavePolicies | Create a leave policy based on an existing leave policy |
| GET | /v2/providers/employers/leavePolicies/{leavePolicyId} | A single leave policy |
| PUT | /v2/providers/employers/leavePolicies/{leavePolicyId} | Edit the details of a leave policy |
| DELETE | /v2/providers/employers/leavePolicies/{leavePolicyId} | Delete a leave policy |
| GET | /v2/providers/employers/leavePolicies/{leavePolicyId}/agebasedleave | Age based leave |
| POST | /v2/providers/employers/leavePolicies/{leavePolicyId}/agebasedleave | Create an age based leave record |
| GET | /v2/providers/employers/leavePolicies/agebasedleave/{ageBasedLeaveId} | An age based leave record |
| PUT | /v2/providers/employers/leavePolicies/agebasedleave/{ageBasedLeaveId} | Edit the details of an age based leave |
| DELETE | /v2/providers/employers/leavePolicies/agebasedleave/{ageBasedLeaveId} | Delete an age based leave record |
| GET | /v2/providers/employers/leavePolicies/{leavePolicyId}/yearsofservicebasedleave | years of service based leave |
| POST | /v2/providers/employers/leavePolicies/{leavePolicyId}/yearsofservicebasedleave | Create a years of service based leave record |
| GET | /v2/providers/employers/leavePolicies/yearsofservicebasedleave/{yearsOfServiceBasedLeaveId} | A years of service based leave record |
| PUT | /v2/providers/employers/leavePolicies/yearsofservicebasedleave/{yearsOfServiceBasedLeaveId} | Edit the details of a years of service based leave |
| DELETE | /v2/providers/employers/leavePolicies/yearsofservicebasedleave/{yearsOfServiceBasedLeaveId} | Delete an years of service based leave record |
| GET | /v2/providers/employers/leavePolicies/{leavePolicyId}/wagebasedleave | Wage based leave |
| POST | /v2/providers/employers/leavePolicies/{leavePolicyId}/wagebasedleave | Create a wage based leave record |
| GET | /v2/providers/employers/leavePolicies/wagebasedleave/{wageBasedLeaveId} | A wage based leave record |
| PUT | /v2/providers/employers/leavePolicies/wagebasedleave/{wageBasedLeaveId} | Edit the details of a wage based leave |
| DELETE | /v2/providers/employers/leavePolicies/wagebasedleave/{wageBasedLeaveId} | Delete a wage based leave record |
| GET | /v2/providers/employers/leavepolicies/{leavePolicyId}/employments | Get list of linked employments for the leave policy |
| PATCH | /v2/providers/employers/leavepolicies/{leavePolicyId}/employments | Create or delete multiple linked employments for the leave policy |
| GET | /v2/providers/employers/leavepolicies/{leavePolicyId}/employments/leave/accrual | Leave accrual for employments of a leave policy |
| GET | /v2/providers/employers/leavepolicies/{leavePolicyId}/employments/{employmentId}/leave/accrual" | Leave accrual for an employment |
| GET | /v2/providers/employers/leavepolicies/{leavePolicyId}/employments/leave/entitlement | Leave entitlement for employments of a leave policy |
| GET | /v2/providers/employers/leavepolicies/{leavePolicyId}/employments/{employmentId}/leave/entitlement" | Leave entitlement for an employment |
| PATCH | /v2/providers/employers/{employerId}/employees/employments/leave/entitlement | Apply the entitlement for multiple employments |
| PATCH | /v2/providers/employers/employees/employments/{employmentId}/leave/entitlement" | Apply the entitlement for an employment |
| GET | /v2/providers/{providerId}/leavePolicies | List of all the leave policies at provider level. |
| POST | /v2/providers/{providerId}/leavePolicies | Create a leave policy |
| GET | /v2/providers/leavePolicies/{leavePolicyId} | A single leave policy |
| PUT | /v2/providers/leavePolicies/{leavePolicyId} | Edit the details of a leave policy |
| DELETE | /v2/providers/leavePolicies/{leavePolicyId} | Delete a leave policy |
| GET | /v2/providers/leavePolicies/{leavePolicyId}/agebasedleave | Age based leave |
| POST | /v2/providers/leavePolicies/{leavePolicyId}/agebasedleave | Create an age based leave record |
| GET | /v2/providers/leavePolicies/agebasedleave/{ageBasedLeaveId} | An age based leave record |
| PUT | /v2/providers/leavePolicies/agebasedleave/{ageBasedLeaveId} | Edit the details of an age based leave |
| DELETE | /v2/providers/leavePolicies/agebasedleave/{ageBasedLeaveId} | Delete an age based leave record |
| GET | /v2/providers/leavePolicies/{leavePolicyId}/yearsofservicebasedleave | years of service based leave |
| POST | /v2/providers/leavePolicies/{leavePolicyId}/yearsofservicebasedleave | Create a years of service based leave record |
| GET | /v2/providers/leavePolicies/yearsofservicebasedleave/{yearsOfServiceBasedLeaveId} | A years of service based leave record |
| PUT | /v2/providers/leavePolicies/yearsofservicebasedleave/{yearsOfServiceBasedLeaveId} | Edit the details of a years of service based leave |
| DELETE | /v2/providers/leavePolicies/yearsofservicebasedleave/{yearsOfServiceBasedLeaveId} | Delete an years of service based leave record |
| GET | /v2/providers/leavePolicies/{leavePolicyId}/wagebasedleave | Wage based leave |
| POST | /v2/providers/leavePolicies/{leavePolicyId}/wagebasedleave | Create a wage based leave record |
| GET | /v2/providers/leavePolicies/agebasedleave/{wageBasedLeaveId} | A wage based leave record |
| PUT | /v2/providers/leavePolicies/agebasedleave/{wageBasedLeaveId} | Edit the details of a wage based leave |
| DELETE | /v2/providers/leavePolicies/agebasedleave/{wageBasedLeaveId} | Delete a wage based leave record |
| GET | /v2/providers/employers/{employerId}/leavetypes | List of leave types |
| GET | /v2/providers/employers/{employerId}/leavetypes/{leaveTypeId} | Details of a leave type |
| PUT | /v2/providers/employers/{employerId}/leavetypes/{leaveTypeId} | Edit the details of a leave type |
| GET | /v2/providers/employers/{employerId}/employees/employments/leaverequests | List of leave requests for the employees of an employer |
| PATCH | /v2/providers/employers/employees/employments/leaverequests | Change the status of leave requests |
| GET | /v2/providers/employers/employees/employments/leaverequests/currentlyAvailableUnits | Currently available units for the given leaveRequestIds |
| GET | /v2/providers/employers/employees/employments/{employmentId}/leave | List of all the leave entries |
| POST | /v2/providers/employers/employees/employments/{employmentId}/leave | Create a leave record for an employment |
| GET | /v2/providers/employers/employees/employments/leave/{leaveId} | A single leave entry |
| PUT | /v2/providers/employers/employees/employments/leave/{leaveId} | Edit the details of a leave |
| DELETE | /v2/providers/employers/employees/employments/leave/{leaveId} | Delete a specific leave record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/leave/metadata | Get the values for the metadata fields |
| GET | /v2/providers/employers/employees/employments/{employmentId}/leave/defaults | Get the default values to be used when POSTing a new record |
| GET | /v2/providers/employers/employees/employments/leave/{leaveId}/metadata | Get the values for the metadata fields |
| GET | /v2/providers/employers/employees/employments/{employmentId}/leave/proposedleavehours | Get the proposed number of leave hours for an employment |
| GET | /v2/providers/employers/{employerId}/leave/proposedleavehours | Get the proposed number of leave hours for all employments of an employer |
| GET | /v2/providers/employers/employees/employments/{employmentId}/leave/overview/{year} | Download the leave overview for an employment and year |
| GET | /v2/providers/employers/employees/employments/{employmentId}/leaverequests | leave requests by employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/leaverequests | Create a leave request for an employment |
| GET | /v2/providers/employers/employees/employments/leaverequests/{leaveRequestId} | Details of a leave request |
| PUT | /v2/providers/employers/employees/employments/leaverequests/{leaveRequestId} | Change the details of a leave request |
| GET | /v2/providers/employers/employees/employments/{employmentId}/leavebalances | List of yearly leave balances for each leave type. |
| GET | /v2/providers/employers/{employerId}/leavebalances | The leave balance for all employments |
| GET | /v2/providers/employers/{employerId}/leavebalances/worth | The leave balanceworth for all employments |
| GET | /v2/providers/employers/{employerId}/leavebalances/grouped | Summed up leave balance total and grouped by |
| GET | /v2/providers/employers/employees/employments/{employmentId}/leavepolicies | Get list of linked leave policies for the employment |
| PATCH | /v2/providers/employers/employees/employments/{employmentId}/leavepolicies | Link or unlink leave policies for the employment |
| GET | /v2/providers/employers/{employerId}/import/leave" | Get data to create an importfile |
| POST | /v2/providers/employers/{employerId}/import/leave" | Import leave via a csv file |
| POST | /v2/providers/employers/{employerId}/leave | Post leave for multiple employments. |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollprocessoverview | Process Information about a payroll on administration level |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollruns | List of payroll runs for an administration |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId} | Details of a payrollrun |
| PATCH | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId} | Change the availableForEmployee data |
| PATCH | /v2/providers/employers/payrolladministrations/payrollruns | Change the status of payrollruns |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/periodreadyforpayroll | Send an email to inform the salary administrator |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/payslips | Download payslips for a payroll run |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/defaultset | Download the default set of downloads for a payroll run |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/paymentoverviews | Download payment overviews for a payroll run |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/wagesheets | Download wage sheets for a payroll run |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/sepafiles | Get a list of SEPA files for a payroll run |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/sepahashes | Get a list of SEPA hashes for a payroll run |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/sepafiles/{sepafileId} | Download a SEPA file |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/totalsepafile | Download a total SEPA file |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/runoverviews | Download run overviews for a payroll run |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/payrollcontrolregister | Download payroll control register for a payroll run |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/journalentriesperdistributionunitoverviews | Download the journal entries by distribution Unit. |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/errorsandwarnings | Download errors and warnings for a payroll run |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/nonsepafile | Download a Non Sepa file |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollPeriodDataAuditTrail | Download the audit trail for the payroll period data |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/employmentPayrollDataAuditTrail | Download the audit trail for the employment payroll data |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollperiods | List of all available payroll periods and runs |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollperiods/minimized | List of all available payroll periods |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollperiods/{payrollPeriodId}/payrollresults | Get payroll results for the given payroll period |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollperiods/compare | Get the results of the given payroll period and the one before |
| GET | /v2/providers/employers/{employerId}/payrollresults/statistics/data | basic payrollresults statistics |
| GET | /v2/providers/employers/{employerId}/employees/employments/payrollperiods/payrollcomponents/{payrollComponent} | Get the results of the given payroll period and the one before |
| GET | /v2/providers/employers/payrolladministrations/payrollperiods/payrollresults/compare | Compare payrollresults for two payrollperiods at providerlevel |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/results | Get results for a payroll run |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/BalanceSheet | Get payroll run balance sheet |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollresults | Payroll results for several periods |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/payrollresults" | Payroll results for a payrollrun |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollperiods/payrollresults" | Download payrollresults in columns |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollperiods/payrollresults/grouped" | Download FTE payrollresults in columns |
| GET | /providers | List of providers |
| GET | /v2/providers/{providerId}/logo | Download the provider logo |
| GET | /v2/providers/{providerId}/logo/{version} | Download the provider logo |
| GET | /v2/providers/{providerId}/contactinformation | Retrieve provider contact information |
| GET | /v2/providers/{providerId}/dashboard | Dashboard for a provider |
| GET | /v2/providers/{providerId}/logos | Logos at providerlevel |
| POST | /v2/providers/{providerId}/logos | Upload a logo for the provider |
| GET | /v2/providers/logos/{logoId} | Logo at providerlevel |
| PUT | /v2/providers/logos/{logoId} | Edit a provider logo |
| DELETE | /v2/providers/logos/{logoId} | Delete a logo at providerlevel |
| GET | /v2/providers/logos/{logoId}/logo | Logo without properties at providerlevel |
| GET | /v2/providers/{providerId}/configuration | Provider configuration |
| PUT | /v2/providers/{providerId}/configuration | Edit provider configuration |
| GET | /v2/providers/{providerId}/configuration/payslip | Provider payslip configuration |
| PUT | /v2/providers/{providerId}/configuration/payslip | Edit provider configuration |
| GET | /v2/providers/{providerId}/configuration/payslip/logo | Provider payslip logo |
| DELETE | /v2/providers/{providerId}/configuration/payslip/logo | Delete the provider payslip logo |
| POST | /v2/providers/{providerId}/configuration/payslip/logo | Upload a logo for the payslip at providerlevel. |
| GET | /v2/providers/{providerId}/notificationsettings | The notification settings for the provider |
| PATCH | /v2/providers/{providerId}/notificationsettings | Manage the Provider notification settings |
| GET | /v2/providers/{providerId}/groupclassifications | List groupclassifications for an provider |
| POST | /v2/providers/{providerId}/groupclassifications | Add a groupclassification for an provider |
| PUT | /v2/providers/groupclassifications/{groupClassificationId} | Edit a groupclassification record |
| DELETE | /v2/providers/groupclassifications/{groupClassificationId} | Delete a groupclassification record |
| GET | /v2/providers/employers/payrolladministrations/workrelatedcostsutilization | WorkrelatedCostsUtilization per administration. |
| GET | /v2/providers/{providerId}/authorizationsets | List of authorization sets |
| POST | /v2/providers/{providerId}/authorizationsets | Create an AuthorizationSet for an provider |
| GET | /v2/providers/authorizationsets/{authorizationSetId} | Details of a authorization set |
| PUT | /v2/providers/authorizationsets/{authorizationSetId} | Edit the details of an authorizationset |
| DELETE | /v2/providers/authorizationsets/{authorizationSetId} | Delete a specific AuthorizationSet |
| GET | /v2/providers/{providerId}/modulesets | List of module sets |
| POST | /v2/providers/{providerId}/modulesets | Create a module set for an provider |
| GET | /v2/providers/modulesets/{moduleSetId} | Details of a module set |
| PATCH | /v2/providers/modulesets/{moduleSetId} | Edit the details of an module set |
| DELETE | /v2/providers/modulesets/{moduleSetId} | Delete a specific module set |
| GET | /v2/providers/employers/{employerId}/moduleset | Get module set for an employer |
| PUT | /v2/providers/employers/{employerId}/moduleset | Update module set for an employer |
| GET | /v2/providers/{providerId}/notificationsets | List of notification sets |
| POST | /v2/providers/{providerId}/notificationsets | Create a notification set for an provider |
| GET | /v2/providers/notificationsets/{notificationSetId} | Details of a notification set |
| PATCH | /v2/providers/notificationsets/{notificationSetId} | Edit the details of an notification set |
| DELETE | /v2/providers/notificationsets/{notificationSetId} | Delete a specific notification set |
| GET | /v2/providers/employers/payrolladministrations/payrollperiods/{payrollPeriodId}/payrollruns/status | Payroll status for each administration. |
| GET | /v2/providers/employers/payrolladministrations/payrollperiods/{payrollPeriodId}/payrolltaxreturns/status" | PayrollTaxreturn status for each wageTaxNumber. |
| GET | /v2/providers/employers/payrolladministrations/payrollperiods/{payrollPeriodId}/pensiondeclaration/status | Pension declaration status for each externalParty. |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/journalruns | List of journal runs for an administration |
| GET | /v2/providers/employers/payrolladministrations/journalruns/{journalrunId} | Details of a journal run |
| PATCH | /v2/providers/employers/payrolladministrations/journalruns/{journalrunId} | Change the status of a journal run |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/journalruns/initiate | Initiate journal run (journaliseren) |
| POST | /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/undo | Undo journal run (verwijderen journaalrun) |
| POST | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/journalruns/recalculate | Recalculate journal for a payroll run |
| GET | /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/results | Get journal results for a journal run |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/journalruns/cumulativeresults | Get journal results for a payroll administration |
| GET | /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/report | Get journal report for a journal run |
| GET | /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/runoverview | Get journal run overview for a journal run |
| GET | /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/runoverviewperemployment | Get journal run overview per employment for a journal run |
| GET | /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/exportAuditTrail | List export attempts for a journal run |
| GET | /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/errors | Errors of a journal run |
| POST | /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/send | Send the journal run |
| POST | /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/download | Download the journal run |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/journalConfigurations | List of journal configurations |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/journalConfigurations | Create a new journal configuration |
| GET | /v2/providers/employers/payrolladministrations/journalConfigurations/{journalConfigurationId} | Details of a journal configuration |
| PUT | /v2/providers/employers/payrolladministrations/journalConfigurations/{journalConfigurationId} | Edit the details of a journal configuration |
| DELETE | /v2/providers/employers/payrolladministrations/journalConfigurations/{journalConfigurationId} | Delete a journal configuration |
| GET | /v2/providers/employers/payrolladministrations/journalConfigurations/{journalConfigurationId}/journalApplication | Get the journal application for a journal configuration |
| POST | /v2/providers/employers/payrolladministrations/journalConfigurations/{journalConfigurationId}/journalApplication | Create a new journal application for a journal configuration |
| PATCH | /v2/providers/employers/payrolladministrations/journalConfigurations/{journalConfigurationId}/journalApplication | Edit the details of a journal application |
| DELETE | /v2/providers/employers/payrolladministrations/journalConfigurations/{journalConfigurationId}/journalApplication | Delete a journal application |
| GET | /v2/providers/{providerId}/journalProfiles | List journal profiles for the given provider |
| POST | /v2/providers/{providerId}/journalProfiles | Create a journal profile for the provider. |
| GET | /v2/providers/journalProfiles/{journalProfileId} | Details of a journal profile |
| PUT | /v2/providers/journalProfiles/{journalProfileId} | Edit the details of a journal profile |
| DELETE | /v2/providers/journalProfiles/{journalProfileId} | Delete a journal profile |
| GET | /v2/providers/journalProfiles/{journalProfileId}/ledgerAccounts | List of ledger accounts for a journal profile of a specific provider. |
| POST | /v2/providers/journalProfiles/{journalProfileId}/ledgerAccounts | Create a new ledger account for a journal profile of a specific provider. |
| GET | /v2/providers/journalProfiles/ledgerAccounts/{ledgerAccountId} | Details of a ledger account at provider level |
| PATCH | /v2/providers/journalProfiles/ledgerAccounts/{ledgerAccountId} | Edit the details of a journal allocation record at the provider level |
| DELETE | /v2/providers/journalProfiles/ledgerAccounts/{ledgerAccountId} | Delete a ledger account on the provider level |
| GET | /v2/providers/journalProfiles/{journalProfileId}/ledgerAccountToPayrollComponentLinks" | List of ledger account to payroll component links at provider level |
| POST | /v2/providers/journalProfiles/{journalProfileId}/ledgerAccountToPayrollComponentLinks" | Create a new ledger account to payroll component link for a journal profile at provider level |
| GET | /v2/providers/journalProfiles/ledgerAccountToPayrollComponentLinks/{ledgerAccountToPayrollComponentLinkId} | Details of a ledger account to payroll component link at provider level |
| PATCH | /v2/providers/journalProfiles/ledgerAccountToPayrollComponentLinks/{ledgerAccountToPayrollComponentLinkId} | Edit the details of a ledger account to payroll component link record at provider level |
| DELETE | /v2/providers/journalProfiles/ledgerAccountToPayrollComponentLinks/{ledgerAccountToPayrollComponentLinkId} | Delete a ledger account to payroll component link at provider level |
| GET | /v2/providers/journalProfiles/{journalProfileId}/costCenters | List of cost centers at provider level |
| POST | /v2/providers/journalProfiles/{journalProfileId}/costCenters | Create a new cost center for a journal profile at provider level |
| GET | /v2/providers/journalProfiles/costCenters/{costCenterId} | Details of a cost center at provider level |
| PATCH | /v2/providers/journalProfiles/costCenters/{costCenterId} | Edit the details of a cost center at provider level |
| DELETE | /v2/providers/journalProfiles/costCenters/{costCenterId} | Delete a cost center at provider level |
| GET | /v2/providers/journalProfiles/{journalProfileId}/costUnits | List of cost units at provider level |
| POST | /v2/providers/journalProfiles/{journalProfileId}/costUnits | Create a new cost unit for a journal profile at provider level |
| GET | /v2/providers/journalProfiles/costUnits/{costUnitId} | Details of a cost unit at provider level |
| PATCH | /v2/providers/journalProfiles/costUnits/{costUnitId} | Edit the details of a cost unit at provider level |
| DELETE | /v2/providers/journalProfiles/costUnits/{costUnitId} | Delete a cost unit at provider level |
| GET | /v2/providers/journalprofiles/{journalProfileId}/CostCenterCostUnitMatrix | Cost center and cost unit matrix |
| PATCH | /v2/providers/journalprofiles/{journalProfileId}/CostCenterCostUnitMatrix | Edit the links between cost center and cost units |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/journalProfiles | List of journal profiles |
| GET | /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId} | Details of a journal profile |
| PATCH | /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId} | Edit the details of a journal profile record |
| GET | /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/ledgerAccounts | List of ledger accounts |
| POST | /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/ledgerAccounts | Create a new ledger account for a journal profile |
| GET | /v2/providers/employers/payrolladministrations/journalProfiles/ledgerAccounts/{ledgerAccountId} | Details of a ledger account |
| PATCH | /v2/providers/employers/payrolladministrations/journalProfiles/ledgerAccounts/{ledgerAccountId} | Edit the details of a journal allocation record |
| DELETE | /v2/providers/employers/payrolladministrations/journalProfiles/ledgerAccounts/{ledgerAccountId} | Delete a ledger account |
| GET | /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/ledgerAccountToPayrollComponentLinks | List of ledger account to payroll component links |
| POST | /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/ledgerAccountToPayrollComponentLinks | Create a new ledger account to payroll component link for a journal profile |
| GET | /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/ledgerAccountToPayrollComponentLinks/metadata | Metadata for ledger account to payroll component links |
| GET | /v2/providers/employers/payrolladministrations/journalProfiles/ledgerAccountToPayrollComponentLinks/{ledgerAccountToPayrollComponentLinkId} | Details of a ledger account to payroll component link |
| PATCH | /v2/providers/employers/payrolladministrations/journalProfiles/ledgerAccountToPayrollComponentLinks/{ledgerAccountToPayrollComponentLinkId} | Edit the details of a ledger account to payroll component link record |
| DELETE | /v2/providers/employers/payrolladministrations/journalProfiles/ledgerAccountToPayrollComponentLinks/{ledgerAccountToPayrollComponentLinkId} | Delete a ledger account to payroll component link |
| GET | /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/costCenters | List of cost centers |
| POST | /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/costCenters | Create a new cost center for a journal profile |
| GET | /v2/providers/employers/payrolladministrations/journalProfiles/costCenters/{costCenterId} | Details of a cost center |
| PATCH | /v2/providers/employers/payrolladministrations/journalProfiles/costCenters/{costCenterId} | Edit the details of a cost center |
| DELETE | /v2/providers/employers/payrolladministrations/journalProfiles/costCenters/{costCenterId} | Delete a cost center |
| GET | /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/costUnits | List of cost units |
| POST | /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/costUnits | Create a new cost unit for a journal profile |
| GET | /v2/providers/employers/payrolladministrations/journalProfiles/costUnits/{costUnitId} | Details of a cost unit |
| PATCH | /v2/providers/employers/payrolladministrations/journalProfiles/costUnits/{costUnitId} | Edit the details of a cost unit record |
| DELETE | /v2/providers/employers/payrolladministrations/journalProfiles/costUnits/{costUnitId} | Delete a cost unit |
| GET | /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/CostCenterCostUnitMatrix | Cost centers and cost unit matrix |
| PATCH | /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/CostCenterCostUnitMatrix | Edit the links between cost centers and cost units |
| GET | /v2/providers/employers/employees/employments/{employmentId}/journalallocations | List of journal allocations for an employment |
| POST | /v2/providers/employers/employees/employments/{employmentId}/journalallocations | Create a new journal allocation record for an employment |
| GET | /v2/providers/employers/employees/employments/journalallocations/{journalAllocationId} | Details of a journal allocation |
| PUT | /v2/providers/employers/employees/employments/journalallocations/{journalAllocationId} | Edit the details of a journal allocation record |
| DELETE | /v2/providers/employers/employees/employments/journalallocations/{journalAllocationId} | Delete a specific journal allocation record |
| GET | /v2/providers/{providerId}/users | List of provider users for an provider |
| POST | /v2/providers/{providerId}/users | Create an SSO or Azure AD provider user for an provider |
| GET | /v2/providers/users/{userId} | Details of a provider user |
| PUT | /v2/providers/users/{userId} | Edit the details of a provider user |
| DELETE | /v2/providers/users/{userId} | Delete a specific provider user record |
| PATCH | /v2/providers/users/{userId}/access | Reinstate or Revoke access to Loket for a provider user (clients) |
| POST | /v2/providers/{providerId}/users/invite | Send an invite to a provider user |
| PATCH | /v2/providers/users/{userId}/invite | Resend or Revoke an invite for a provider user |
| GET | /v2/providers/users/{userId}/authorizations | The authorizations for the provider user |
| PATCH | /v2/providers/users/{userId}/authorizations | Manage the Provider user authorizations |
| GET | /v2/providers/users/{userId}/authorizationSet | The authorization set for the user for the Provider |
| GET | /v2/providers/users/{userId}/authorizationGroups | The authorization groups for the provider user |
| PATCH | /v2/providers/users/{userId}/authorizationGroups | Manage the provider user authorization groups |
| GET | /v2/providers/users/{userId}/clients | List of all the clients for the provider user |
| GET | /v2/providers/{providerId}/authorizationgroups | List authorization groups (teams) for the given provider |
| POST | /v2/providers/{providerId}/authorizationgroups | Create an authorization group (team) for the provider. |
| GET | /v2/providers/authorizationgroups/{authorizationGroupId} | Details of an authorization group |
| PUT | /v2/providers/authorizationgroups/{authorizationGroupId} | Edit the details of an authorization group |
| DELETE | /v2/providers/authorizationgroups/{authorizationGroupId} | Delete an authorization group |
| GET | /v2/providers/authorizationgroups/{authorizationGroupId}/authorizations | The authorizations for the authorization group |
| PATCH | /v2/providers/authorizationgroups/{authorizationGroupId}/authorizations | Manage the authorization group authorizations |
| GET | /v2/providers/authorizationgroups/{authorizationGroupId}/employers | The employers for the authorization group |
| PATCH | /v2/providers/authorizationgroups/{authorizationGroupId}/employers | Manage the authorization group employers |
| GET | /v2/providers/authorizationgroups/{authorizationGroupId}/users | The users for the authorization group |
| PATCH | /v2/providers/authorizationgroups/{authorizationGroupId}/users | Manage the authorization group users |
| GET | /v2/providers/{providerId}/employers/{employerId}/authorizationGroups | The authorization groups for the employer |
| PATCH | /v2/providers/{providerId}/employers/{employerId}/authorizationGroups | Manage the authorization groups linked to the employer |
| GET | /v2/providers/employers/users/{userId}/integrations | List of all the integrations for the employer user |
| PUT | /v2/providers/employers/users/{userId}/integrations/{applicationId} | Change an integration |
| DELETE | /v2/providers/employers/users/{userId}/integrations/{applicationId} | Delete an integration |
| GET | /v2/providers/employers/users/{userId}/integrations/{applicationId}/logo | Download the application logo |
| GET | /v2/providers/users/{userId}/integrations | List of all the integrations for a provider user |
| PUT | /v2/providers/users/{userId}/integrations/{applicationId} | Change an integration for a provider user |
| DELETE | /v2/providers/users/{userId}/integrations/{applicationId} | Delete an integration for a provider user |
| GET | /v2/providers/users/{userId}/integrations/{applicationId}/logo | Download the application logo |
| GET | /v2/providers/employers/users/{userId}/clients | List of all the clients for the employer user |
| GET | /v2/providers/users/{userId}/connectedApplications | List of all the connected applications for the logon user |
| PATCH | /v2/providers/users/{userId}/connectedApplications/initiate | Initiate the OAuth flow to connect to an application |
| PATCH | /v2/providers/users/{userId}/connectedApplications/refresh | Initiate the OAuth flow to refresh a connection for an application |
| DELETE | /v2/providers/users/connectedApplications/{connectedApplicationId} | Delete a connected application |
| GET | /v2/providers/employers/{employerId}/users | List of users for an employer |
| POST | /v2/providers/employers/{employerId}/users | Create an SSO or Azure AD user for an employer |
| PATCH | /v2/providers/employers/users/{userId}/access | Reinstate or Revoke access to Loket for an employer user (clients) |
| POST | /v2/providers/employers/{employerId}/users/invite | Send an invite to an email address to create an employer user |
| PATCH | /v2/providers/employers/users/{userId}/invite | Resend or Revoke an invite for an employer user |
| GET | /v2/providers/employers/users/{userId} | Details of an employer user |
| PUT | /v2/providers/employers/users/{userId} | Edit the details of an employer user user |
| DELETE | /v2/providers/employers/users/{userId} | Delete a specific employer user record |
| GET | /v2/providers/employers/{employerId}/users/{userId}/informationForDelete | Information about the employer user to determine if the user can be deleted |
| DELETE | /v2/providers/employers/{employerId}/users/{userId} | unlink employer user and employer |
| GET | /v2/providers/{providerId}/employers/users | List of all employer users for the provider |
| GET | /v2/providers/employers/users/{userId}/employers | List of employers linked to the user |
| GET | /v2/providers/employers/{employerId}/users/departments | Get the list of departments that the user has access to |
| PATCH | /v2/providers/employers/{employerId}/users/{userId}/departments | Link or unlink departments from an user. |
| GET | /v2/providers/employers/users/{userId}/notificationsettings | The notification settings for the user |
| PATCH | /v2/providers/employers/users/{userId}/notificationsettings | Manage the employer user notification settings |
| GET | /v2/providers/employers/users/{userId}/notificationset | The notification set for the user |
| GET | /v2/providers/employers/{employerId}/users/{userId}/authorizations | The authorizations for the user |
| PATCH | /v2/providers/employers/{employerId}/users/{userId}/authorizations | Manage the employer user authorizations |
| GET | /v2/providers/employers/{employerId}/users/{userId}/authorizationSet | The authorization set for the user for the employer |
| POST | /v2/providers/employers/{employerId}/users/link | Link an existing employer user to this employer. |
| GET | /v2/providers/employers/{employerId}/recommendedactions | List of recommended actions for an employer, per logged on user |
| GET | /v2/providers/employers/{employerId}/users/{userId}/employee | Get the Employee linked to the user. |
| PATCH | /v2/providers/employers/{employerId}/users/{userId}/employee | Link or unlink Employee from an user. |
| GET | /v2/providers/{providerId}/userResponsibilities | List of user responsibilities for the provider |
| POST | /v2/providers/{providerId}/userResponsibilities | Create an user responsibility for a provider |
| PUT | /v2/providers/{providerId}/userResponsibilities/{userResponsibilityId} | Edit an user responsibility |
| GET | /v2/providers/employers/{employerId}/userResponsibilities | List of user responsibilities for the employer |
| GET | /v2/providers/employers/{employerId}/userResponsibilities/{userResponsibilityId}/users | List of employer users and their linked status to the user responsibility for the given employer |
| PATCH | /v2/providers/employers/{employerId}/userResponsibilities/{userResponsibilityId}/users | Manage the users linked to the user responsibility |
| GET | /v2/providers/employers/{employerId}/users/{userId}/userResponsibilities | List of responsibilities for the user |
| PATCH | /v2/providers/employers/{employerId}/users/{userId}/userResponsibilities | Manage the responsibilities linked to the user |
| GET | /v2/providers/employers/{employerId}/dashboardLicenses | Get the list dashboard licenses |
| PUT | /v2/providers/employers/{employerId}/dashboardLicenses | Edit the dashboard license |
| GET | /v2/providers/{providerId}/externaltenants | Get available external tenants (provider scope) |
| GET | /v2/providers/employers/{employerId}/externaltenants | Get available external tenants (employer scope) |
| GET | /v2/providers/users/{providerUserId}/configuredexternaltenant | Configured external tenant for a provider user |
| PATCH | /v2/providers/users/{providerUserId}/configuredexternaltenant | Add an external tenant for a provider user |
| GET | /v2/providers/employers/users/{employerUserId}/configuredexternaltenant | Configured external tenant for an employer user |
| PATCH | /v2/providers/employers/users/{employerUserId}/configuredexternaltenant | Add an external tenant for an employer user |
| GET | /v2/providers/employers/employees/employments/{employmentId}/payslips | List of payslips for an employment |
| GET | /v2/providers/employers/employees/employments/{employmentId}/payslips/{year} | Download payslips for an employment and year |
| GET | /v2/providers/employers/employees/employments/{employmentId}/payslips/{payrollrunId} | Download payslips of an employment for a payrollrun |
| GET | /v2/providers/employers/employees/employments/{employmentId}/payrollperiodresults/year/{year} | Get payroll period results of an employment for a year |
| GET | /v2/providers/employers/employees/employments/{employmentId}/payslips/summary/{payrollPeriodId} | Download a cummulative payslip for a single payroll period |
| GET | /v2/providers/employers/employees/employments/{employmentId}/wagesheet/{year} | Download wage sheets for an employment |
| GET | /v2/providers/employers/employees/employments/{employmentId}/yearendstatements | Year-end statements for the employment |
| GET | /v2/providers/employers/employees/employments/{employmentId}/yearendstatements/{year} | Download year-end statement of an employment for a year |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/yearendstatements | Year-end statements for the payroll administration |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/yearendstatements/{year} | Download year-end statement of a payroll administration for a year |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrolltaxreturns | List of tax returns for an administration |
| PATCH | /v2/providers/employers/payrolladministrations/payrolltaxreturns | Change the status of payroll tax returns |
| GET | /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}/overview | Download the overview report of a payroll tax return |
| GET | /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}/message | Download the message of a payroll tax return |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrolltaxreturns/{payrolltaxreturnId}/sepafile | Download the SEPA file for a payroll tax return |
| GET | /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}/sepahash | Get a SEPA hash for a payroll tax return |
| GET | /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId} | Details of a tax return for an administration |
| GET | /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}/ideal | Pay payroll taxes using IDEAL |
| GET | /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}/idealPaymentStatus | Get the status of the IDEAL payment |
| GET | /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}/report | Get payroll tax return report |
| POST | /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}/sendresponsemessage | Send the response message for the payroll tax return |
| PATCH | /v2/providers/employers/payrolladministrations/payrolltaxreturns/{messageReference} | Change the status of payroll tax returns |
| POST | /v2/providers/employers/payrolladministrations/payrolltaxreturns/{messageReference}/sendresponsemessagebymessagereference | Send the response message for the payroll tax return |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrolltaxreturns/initiate | Initiate payroll tax return (aanmaken loonaangifte) |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrolltaxreturns/initiateForPreviousYear | Initiate payroll tax return for a closed year (aanmaken loonaangifte voorgaand jaar) |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrolltaxreturns/initiateAnnual | Initiate an annual payroll tax return |
| POST | /v2/providers/employers/payrolladministrations/payrollperiods/{payrollPeriodId}/payrolltaxreturns | Initiate payroll tax return Collective |
| PATCH | /v2/providers/employers/payrolladministrations/payrollperiods/{payrollPeriodId}/payrolltaxreturns | Update payroll tax return status Collective |
| POST | /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}/undo | Undo payroll tax return (verwijderen loonaangifte) |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrolltaxreturns/withdrawIncomeRelationshipNumber | Add a withdraw an income relationship number to an open payroll tax return |
| PATCH | /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}/resend | Resend payroll tax return (Herzenden loonaangifte) |
| GET | /v2/providers/employers/{employerId}/datanewbusinesstoken | Get Data New Business token for an employer |
| GET | /v2/providers/employers/{employerId}/employees/employments/calendar/availablehours | List available hours per employment (for calendar) |
| GET | /v2/providers/employers/{employerId}/employees/employments/calendar/leave | List leave per employment (for calendar) |
| GET | /v2/providers/employers/{employerId}/employees/employments/calendar/leaverequests | List leave requests per employment (for calendar) |
| GET | /v2/providers/employers/{employerId}/employees/employments/calendar/revokeleaverequests | List leave requests per employment (for calendar) |
| GET | /v2/providers/employers/{employerId}/employees/employments/calendar/absences | List absences per employment (for calendar) |
| GET | /v2/providers/employers/employees/employments/{employmentId}/teamCalendar | Get the calendar data of the department of the employment |
| GET | /v2/providers/employers/employees/employments/{employmentId}/personalCalendar | Gets the personal calendar |
| GET | /v2/providers/employers/{employerId}/employmenttemplates | Employment templates |
| POST | /v2/providers/employers/{employerId}/employmenttemplates | Create an Employment template for an employer |
| PUT | /v2/providers/employers/employmenttemplates/{employmenttemplateId} | Edit the details of an employment template |
| DELETE | /v2/providers/employers/employmenttemplates/{employmenttemplateId} | Delete a employment template |
| GET | /v2/providers/employers/{employerId}/employees/employments/declarations | List of declarations for the employees of an employer |
| PATCH | /v2/providers/employers/employees/employments/declarations/review | Review (accept or reject) open declarations |
| PATCH | /v2/providers/employers/employees/employments/declarations/process | Process approved declarations |
| GET | /v2/providers/employers/employees/employments/declarations/{declarationId}/attachment | Download attachment |
| POST | /v2/providers/employers/employees/employments/declarations/{declarationId}/attachment | Upload attachment |
| GET | /v2/providers/employers/{employerId}/employees/employments/declarations/withattachment | Get a list of declarations with attachment |
| GET | /v2/providers/employers/employees/employments/{employmentId}/declarations/withattachment | Get a list of declarations with attachment |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollperiods/initialise | Initialise Payroll Period (automatische processen) |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollruns/initiate | Initiate payroll run (verlonen) |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollruns/{payrollPeriodId}/initiationvalues | Initiationvalues of a payrollrun |
| POST | /v2/providers/employers/payrolladministrations/payrollperiods/{payrollPeriodId}/payrollruns | Initiate payroll run Collective |
| PATCH | /v2/providers/employers/payrolladministrations/payrollperiods/{payrollPeriodId}/payrollruns | Update payroll run status Collective |
| POST | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/undo | Undo payroll run (verwijderen loonrun) |
| GET | /v2/providers/employers/employees/employments/{employmentId}/transitioncompensation/calculate/defaults | Get default input parameters transition compensation |
| POST | /v2/providers/employers/employees/employments/{employmentId}/transitioncompensation/calculate | Calculate transition compensation |
| GET | /v2/providers/employers/employees/employments/{employmentId}/documents | Get a list of employment dossier documents |
| POST | /v2/providers/employers/employees/employments/{employmentId}/documents | Upload a document to the employment dossier |
| GET | /v2/providers/employers/employees/employments/{employmentId}/documents/{documentId} | Download employment dossier document |
| DELETE | /v2/providers/employers/employees/employments/{employmentId}/documents/{documentId} | Delete a document in the employment dossier |
| PUT | /v2/providers/employers/employees/employments/{employmentId}/documents/{documentId} | Edit the details of an employment dossier document |
| GET | /v2/providers/employers/employees/employments/{employmentId}/documents/{documentId}/audittrail | Get audittrail for the document in the employment dossier |
| GET | /v2/providers/employers/{employerId}/documents/{documentId} | Download employer dossier document |
| DELETE | /v2/providers/employers/{employerId}/documents/{documentId} | Delete a document in the employer dossier |
| PUT | /v2/providers/employers/{employerId}/documents/{documentId} | Edit the details of an employer dossier document |
| GET | /v2/providers/employers/{employerId}/documents | Get a list of employer dossier documents |
| POST | /v2/providers/employers/{employerId}/documents | Upload a document to the employer dossier |
| GET | /v2/providers/employers/{employerId}/documents/{documentId}/audittrail | Get audittrail for the document in the employer dossier |
| GET | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents/{documentId} | Download concept employee dossier document |
| DELETE | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents/{documentId} | Delete a document in the concept employee dossier |
| PUT | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents/{documentId} | Edit the details of an concept employee dossier document |
| GET | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents | Get a list of concept employee dossier documents |
| POST | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents | Upload a document to the concept employee dossier |
| GET | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents/{documentId}/audittrail | Get audittrail for the document in the concept employee dossier |
| GET | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/dossier" | Document count |
| DELETE | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/dossier" | Delete the complete concept employee dossier |
| GET | /v2/providers/employers/{employerId}/documenttemplates/{documentId} | Download template document |
| DELETE | /v2/providers/employers/{employerId}/documenttemplates/{documentId} | Delete a document template in the employer dossier |
| PUT | /v2/providers/employers/{employerId}/documenttemplates/{documentId} | Edit the details of an document template |
| GET | /v2/providers/employers/{employerId}/documenttemplates | Get a list of document templates |
| POST | /v2/providers/employers/{employerId}/documenttemplates | Upload a document template to the employer dossier |
| POST | /v2/providers/employers/employees/employments/{employmentId}/documenttemplates/{documentId}/generatedocument/preview | Generate a document for an employment - preview |
| POST | /v2/providers/employers/employees/employments/{employmentId}/documenttemplates/{documentId}/generatedocument | Generate a document for an employment |
| POST | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documenttemplates/{documentId}/generatedocument/preview | Generate a document for an concept employee - preview |
| POST | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documenttemplates/{documentId}/generatedocument | Generate a document for an concept employee |
| POST | /v2/providers/employers/{employerId}/documenttemplates/{documentId}/generatedocuments | Generate documents for selected employments |
| GET | /v2/providers/employers/{employerId}/signature/report | Download signature report for an employer |
| POST | /v2/providers/employers/employees/employments/{employmentId}/documents/{documentId}/signature/initiate | Initiate signature - Employment |
| GET | /v2/providers/employers/employees/employments/{employmentId}/documents/{documentId}/signature | Signature details - Employment |
| DELETE | /v2/providers/employers/employees/employments/{employmentId}/documents/{documentId}/signature | Delete signature - Employment |
| GET | /v2/providers/employers/employees/employments/{employmentId}/documents/{documentId}/signature/report | Retrieve the report of the signing - Employment |
| POST | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents/{documentId}/signature/initiate | Initiate signature - Conceptemployee |
| GET | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents/{documentId}/signature | Signature details - Conceptemployee |
| DELETE | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents/{documentId}/signature | Delete signature - Conceptemployee |
| GET | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents/{documentId}/signature/report | Retrieve the report of the signing - Conceptemployee |
| GET | /v2/providers/employers/{employerId}/documents/authorizations | List of authorizations |
| PUT | /v2/providers/employers/{employerId}/documents/authorizations | Edit the authorization matrix |
| POST | /v2/providers/employers/{employerId}/documents/completedossier/initiate | Generate complete dossier |
| DELETE | /v2/providers/employers/{employerId}/documents/completedossier | Delete complete dossier |
| GET | /v2/providers/employers/{employerId}/dossier/report | Download dossier information for an employer |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/apgpensiondeclarations | List of APG pension declarations for an administration |
| GET | /v2/providers/employers/payrolladministrations/apgpensiondeclarations/{apgPensionDeclarationId} | Detail APG pension declaration for an administration |
| PATCH | /v2/providers/employers/payrolladministrations/apgpensiondeclarations/{apgPensionDeclarationId} | Change the status of a apg pension declaration |
| GET | /v2/providers/employers/payrolladministrations/apgpensiondeclarations/{apgPensionDeclarationId}/overview | Download the overview report of an APG pension declaration |
| GET | /v2/providers/employers/payrolladministrations/apgpensiondeclarations/{apgPensionDeclarationId}/message | Download the message of a of an APG pension declaration |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/apgpensiondeclarations/initiate | Initiate a APG pension declaration |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/apgpensiondeclarations/initiateForPreviousYear | Initiate APG pension declaration for a closed year (aanmaken pensioenaangifte voorgaand jaar) |
| POST | /v2/providers/employers/payrolladministrations/apgpensiondeclarations/{apgPensionDeclarationId}/undo | Undo APG pension declaration(verwijderen pensioenaangifte) |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/upapensiondeclarations | List of UPA pension declarations |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/externalparties/{externalPartyKey}/upapensiondeclarations/initiateforpreviousyear | Initiate UPA pension declaration for a closed year (aanmaken pensioenaangifte voorgaand jaar) |
| GET | /v2/providers/employers/payrolladministrations/upapensiondeclarations/{upaPensionDeclarationId} | Detail UPA pension declaration |
| PATCH | /v2/providers/employers/payrolladministrations/upapensiondeclarations/{upaPensionDeclarationId} | Change the status of a upa pension declaration |
| POST | /v2/providers/employers/payrolladministrations/upapensiondeclarations/{upaPensionDeclarationId}/undo | Undo upa pension declaration(verwijderen pensioenaangifte) |
| GET | /v2/providers/employers/payrolladministrations/upapensiondeclarations/{upaPensionDeclarationId}/message | Download the message of a of an UPA pension declaration |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/externalparties/{externalPartyKey}/upapensiondeclarations/initiate | Initiate a UPA pension declaration |
| POST | /v2/providers/employers/payrolladministrations/payrollperiods/{payrollPeriodId}/pensiondeclarations | Initiate pension declaration Collective |
| PATCH | /v2/providers/employers/payrolladministrations/payrollperiods/{payrollPeriodId}/pensiondeclarations | Update pension declaration status Collective |
| GET | /v2/providers/{providerId}/ExternalPartyIdentifications | List of identification data for external parties |
| POST | /v2/providers/{providerId}/ExternalPartyIdentifications | Add the identification data for an external party for a provider |
| GET | /v2/providers/ExternalPartyIdentifications/{externalPartyIdentificationId} | Details of an external party identification for a provider |
| PUT | /v2/providers/ExternalPartyIdentifications/{externalPartyIdentificationId} | Edit an external party identification record |
| DELETE | /v2/providers/ExternalPartyIdentifications/{externalPartyIdentificationId} | Delete an external party identification record |
| GET | /v2/providers/employers/payrollAdministrations/{payrollAdministrationId}/ExternalPartyIdentifications" | List of identification data for external parties on payroll administration level |
| POST | /v2/providers/employers/payrollAdministrations/{payrollAdministrationId}/ExternalPartyIdentifications" | Add the identification data for an external party for a payroll administration |
| GET | /v2/providers/employers/payrollAdministrations/ExternalPartyIdentifications/{externalPartyIdentificationId} | Details of an external party identification for a payroll administration |
| PUT | /v2/providers/employers/payrollAdministrations/ExternalPartyIdentifications/{externalPartyIdentificationId} | Edit an external party identification record |
| DELETE | /v2/providers/employers/payrollAdministrations/ExternalPartyIdentifications/{externalPartyIdentificationId} | Delete an external party identification record |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pawwdeclarations | List of Paww declarations |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pawwdeclarations/initiate | Initiate a Paww declaration |
| GET | /v2/providers/employers/payrolladministrations/pawwdeclarations/{pawwDeclarationId} | Detail Paww declaration |
| PATCH | /v2/providers/employers/payrolladministrations/pawwdeclarations/{pawwDeclarationId} | Change the status of a Paww declaration |
| GET | /v2/providers/employers/payrolladministrations/pawwdeclarations/{pawwDeclarationId}/message | Download the message of a of an Paww declaration |
| POST | /v2/providers/employers/payrolladministrations/pawwdeclarations/{pawwDeclarationId}/undo" | Undo PAWW declaration(deactiveer PAWW aangifte) |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Stipp/initiationvalues | Pension wage statement process initiation values for STIPP |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Stipp/payrollRuns | List of all the payroll runs for the pension wage statement STIPP |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Stipp | Download a pension wage statement for STIPP |
| DELETE | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Stipp | Delete the last created pension wage statement for STIPP |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Stipp | Download the pension wage statement report for STIPP |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Pggm/initiationvalues | Pension wage statement process initiation values for PGGM |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Pggm/payrollRuns | List of all the payroll runs for the pension wage statement PGGM |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Pggm | Download a pension wage statement for PGGM |
| DELETE | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Pggm | Delete the last created pension wage statement for PGGM |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Pggm | Download the pension wage statement report for PGGM |
| GET | /v2/providers/employers/users/downloadrequests | List of download requests for an employment |
| POST | /v2/providers/employers/users/downloadrequests | Create a download request |
| GET | /v2/providers/employers/users/downloadrequests/{downloadRequestId} | Details of a download request record |
| DELETE | /v2/providers/employers/users/downloadrequests/{downloadRequestId} | Delete a specific download request record |
| GET | /v2/providers/employers/users/downloadrequests/{downloadRequestId}/file | Download file of download request |
| GET | /v2/providers/employers/{employerId}/notes | Get a list of notes for an employer. |
| POST | /v2/providers/employers/{employerId}/notes | Add a note for an employer |
| GET | /v2/providers/employers/notes/{noteId} | Details of an employer note |
| PUT | /v2/providers/employers/notes/{noteId} | Edit an employer note record |
| DELETE | /v2/providers/employers/notes/{noteId} | Delete an employer note record |
| GET | /v2/providers/employers/employees/{employeeId}/notes | Get a list of notes for an employee. |
| POST | /v2/providers/employers/employees/{employeeId}/notes | Add a note for an employee |
| GET | /v2/providers/employers/employees/notes/{noteId} | Details of an employee note |
| PUT | /v2/providers/employers/employees/notes/{noteId} | Edit an employee note record |
| DELETE | /v2/providers/employers/employees/notes/{noteId} | Delete an employee note record |
| GET | /v2/providers/employers/{employerId}/employees/notes | Get a list of employee notes for an employer. |
| GET | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/notes | Get a list of notes for an conceptemployee. |
| POST | /v2/providers/employers/conceptemployees/{conceptEmployeeId}/notes | Add a note for an conceptemployee |
| GET | /v2/providers/employers/conceptemployees/notes/{noteId} | Details of an conceptemployee note |
| PUT | /v2/providers/employers/conceptemployees/notes/{noteId} | Edit an conceptemployee note record |
| DELETE | /v2/providers/employers/conceptemployees/notes/{noteId} | Delete an conceptemployee note record |
| GET | /v2/providers/employers/employees/employments/{employmentId}/notes | Get a list of notes for an employment. |
| POST | /v2/providers/employers/employees/employments/{employmentId}/notes | Add a note for an employment |
| GET | /v2/providers/employers/employees/employments/notes/{noteId} | Details of an employment note |
| PUT | /v2/providers/employers/employees/employments/notes/{noteId} | Edit an employment note record |
| DELETE | /v2/providers/employers/employees/employments/notes/{noteId} | Delete an employment note record |
| GET | /v2/providers/employers/{employerId}/employees/employments/notes | Get a list of employment notes for an employer. |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/notes | Get a list of notes for a payroll run. |
| POST | /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/notes | Add a note for a payroll run |
| GET | /v2/providers/employers/payrolladministrations/payrollruns/notes/{noteId} | Details of a payroll run note |
| PUT | /v2/providers/employers/payrolladministrations/payrollruns/notes/{noteId} | Edit a payroll run note record |
| DELETE | /v2/providers/employers/payrolladministrations/payrollruns/notes/{noteId} | Delete a payroll run note record |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollruns/notes | Get a list of payrollrun notes for an payrolladministration. |
| GET | /v2/providers/employers/lastmodifiedversionnumbers | List of employer last modified version numbers |
| GET | /v2/providers/employers/{employerId}/employees/employments/lastmodifiedversionnumbers | List of employment version numbers |
| GET | /v2/providers/{providerId}/emailtemplates | List email templates for an provider |
| GET | /v2/providers/{providerId}/emailtemplates/{emailTemplateId} | Details of an provider email template |
| PUT | /v2/providers/{providerId}/emailtemplates/{emailTemplateId} | Edit an email template record at provider level |
| DELETE | /v2/providers/{providerId}/emailtemplates/{emailTemplateId} | Delete an email template record |
| GET | /v2/providers/employers/{employerId}/emailtemplates | List email templates for an employer |
| GET | /v2/providers/employers/{employerId}/emailtemplates/{emailTemplateId} | Details of an email template |
| PUT | /v2/providers/employers/{employerId}/emailtemplates/{emailTemplateId} | Edit an employer email template record |
| DELETE | /v2/providers/employers/{employerId}/emailtemplates/{emailTemplateId} | Delete an email template record |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/eventnotificationconfigurations | The event notification configuration for a payroll administration |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/eventnotificationconfigurations/{eventTypeId} | Details of an event notification configuration for a payroll administration |
| PUT | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/eventnotificationconfigurations/{eventTypeId} | Edit an event notification configuration for a payroll administration |
| DELETE | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/eventnotificationconfigurations/{eventTypeId} | Delete an event notification configuration for a payroll administration |
| GET | /v2/providers/{providerId}/eventnotificationconfigurations | The event notification configuration for a provider |
| GET | /v2/providers/{providerId}/eventnotificationconfigurations/{eventTypeId} | Details of an event notification configuration for a provider |
| PUT | /v2/providers/{providerId}/eventnotificationconfigurations/{eventTypeId} | Edit an event notification configuration for a provider |
| DELETE | /v2/providers/{providerId}/eventnotificationconfigurations/{eventTypeId} | Delete an event notification configuration for a provider |
| GET | /v2/providers/employers/{employerId}/applications | List of all the applications available to the employer |
| GET | /v2/providers/employers/{employerId}/applications/{applicationId}/users | List of all the users linking the applications and the employer |
| POST | /v2/providers/employers/{employerId}/applications/{applicationId}/registerInterest" | Register a users interest for a marketplace entry |
| GET | /v2/providers/employers/{employerId}/auditTrail/employerData | Get the employer data audit trail |
| GET | /v2/providers/employers/{employerId}/auditTrail/employeeData | Get the employee data audit trail |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/auditTrail/PayrollPeriodData | Get payroll period data audit trail |
| GET | /v2/providers/employers/employees/employments/{employmentId}/payrollSimulatorData | Overview of the data used in a payroll simulation |
| GET | /v2/providers/{providerId}/emailidentities | List of EmailIdentities for a provider |
| POST | /v2/providers/{providerId}/emailidentities | Create an EmailIdentity for a provider |
| DELETE | /v2/providers/emailidentities/{emailIdentityId} | Delete an EmailIdentity for a provider |
| POST | /v2/providers/emailidentities/{emailIdentityId}/sendtestemail | Provider emailIdentity test email |
| POST | /v2/providers/{providerId}/emailidentities/verify | Verify an EmailIdentity for a provider |
| GET | /v2/providers/employers/{employerId}/emailidentities | List of EmailIdentities for an employer |
| POST | /v2/providers/employers/{employerId}/emailidentities | Create an EmailIdentity for an employer |
| DELETE | /v2/providers/employers/emailidentities/{emailIdentityId} | Delete an EmailIdentity for an employer |
| POST | /v2/providers/employers/emailidentities/{emailIdentityId}/sendtestemail | Employer emailIdentity test email |
| POST | /v2/providers/employers/{employerId}/emailidentities/verify | Verify an EmailIdentity for an employer |
| PATCH | /v2/providers/employers/conceptemployees/import/{payrollAdministrationId} | Import concept employees via a file |
| POST | /v2/providers/employers/payrollAdministrations/{payrollAdministrationId}/import/employees | Import employee via a csv file |
| GET | /v2/providers/employers/{employerId}/employees/employments/WageProposals | List of wage proposals for the employments of an employer |
| PATCH | /v2/providers/employers/employees/employments/WageProposals | Accept or reject wage proposals |
| PATCH | /v2/providers/employers/payrollAdministrations/{payrollAdministrationId}/mdvNotifications | MDV notifications |
| POST | /v2/providers/employers/{employerId}/proforma/initialize | Initialize the proforma environment |
| GET | /v2/providers/employers/{employerId}/proforma | Get the status of proforma for this employer |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/workRelatedCostsSchemeFinancials | List of work related costs scheme (WKR) |
| POST | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/workRelatedCostsSchemeFinancials | Create a work related costs scheme financial (WKR) record |
| GET | /v2/providers/employers/payrolladministrations/workRelatedCostsSchemeFinancials/{workRelatedCostsSchemeFinancialId} | Details of a work related costs scheme financial (WKR) |
| PUT | /v2/providers/employers/payrolladministrations/workRelatedCostsSchemeFinancials/{workRelatedCostsSchemeFinancialId} | Edit the details of a work related costs scheme financial record |
| DELETE | /v2/providers/employers/payrolladministrations/workRelatedCostsSchemeFinancials/{workRelatedCostsSchemeFinancialId} | Delete a work related costs scheme financial |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/workRelatedCostsSchemeMatrix | Work related costs scheme matrix (WKR) |
| GET | /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/workRelatedCostsSchemeReport | Download the work related costs scheme report |

### automaticpayroll
| Method | Path | Description |
|--------|------|-------------|
| GET | /automaticpayroll/payrolladministrations/{payrollAdministrationId}/automaticpayrollconfiguration | Automatic payroll configuration |
| PATCH | /automaticpayroll/payrolladministrations/{payrollAdministrationId}/automaticpayrollconfiguration | edit the automatic payroll configuration |
| GET | /automaticpayroll/payrolladministrations/years/{yearId}/automaticpayrolldates | Automatic payroll dates |
| POST | /automaticpayroll/payrolladministrations/years/{yearId}/automaticpayrolldates | create a new automatic payroll date |
| PATCH | /automaticpayroll/payrolladministrations/years/automaticpayrolldates/{automaticPayrollDateId} | edit an automatic payroll date |
| DELETE | /automaticpayroll/payrolladministrations/years/automaticpayrolldates/{automaticPayrollDateId} | delete an automatic payroll date |

### authorizationmodel
| Method | Path | Description |
|--------|------|-------------|
| GET | /authorizationmodel | The authorization model |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users/collectiveactions | List of collective actions for a user |
| GET | /users/collectiveactions/{collectiveActionId} | List of messages of a collective action |
| GET | /users/initiatedworkflows | Workflows initiated by the user |
| GET | /users/yourcampus | Get Yourcampus URL for a user |
| GET | /users/integrations | List of all the integrations for the logon user |
| GET | /users/clients | List of all the clients for the logon user |
| GET | /users/connectedApplications | List of all the connected applications for the logon user |
| PATCH | /users/connectedApplications | Finish the OAuth flow for a connected application |
| PATCH | /users/connectedApplications/initiate | Initiate the OAuth flow to connect to an application |
| PATCH | /users/connectedApplications/refresh | Initiate the OAuth flow to refresh a connection for an application |
| DELETE | /users/connectedApplications/{connectedApplicationId} | Delete a connected application |

### payrollcomponent
| Method | Path | Description |
|--------|------|-------------|
| POST | /payrollcomponent/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollPeriods/{payrollPeriodId}/payrollperioddata/smartpaste | Initiate a Smart Paste on payroll period data on administration level |
| GET | /payrollcomponent/providers/employers/payrolladministrations/payrollPeriods/payrollperioddata/smartpaste/{smartPasteId} | Results of Smart Paste on payroll period data |

### qwoatermicroservice
| Method | Path | Description |
|--------|------|-------------|
| GET | /qwoatermicroservice/providers/employers/employees/employments/{employmentId}/workflows/withattachment | Check if a list of workflowId's for an employment have an attachment |
| GET | /qwoatermicroservice/providers/employers/{employerId}/employees/employments/workflows/withattachment | Check if a list of workflowId's for an employer have an attachment |
| GET | /qwoatermicroservice/providers/employers/dossier/usage | Dossier Usage per employer. |
| GET | /qwoatermicroservice/providers/employers/signature/usage | Signature usage per employer. |
| GET | /qwoatermicroservice/providers/employers/employees/employments/declarations/withattachment | attachment indication for a set of declarationIds |

### billing
| Method | Path | Description |
|--------|------|-------------|
| GET | /billing/providers/employers/{employerId}/billableitems | List of billable items for an employer |
| GET | /billing/providers/{providerId}/billableitems | Overview of number of billable items per employer |

### year
| Method | Path | Description |
|--------|------|-------------|
| PATCH | /year/providers/employers/payrolladministrations/{payrollAdministrationId}/years/{yearId}/requestyeartransition | Request year transition |
| PATCH | /year/providers/employers/payrolladministrations/years/{yearId}/undorequestyeartransition | Undo request year transition |
| POST | /year/providers/employers/payrolladministrations/years/{yearId}/requestyeartransition | Request year transition collective |
| GET | /year/providers/employers/payrolladministrations/years/{year}/status | Year status for each administration |

### person
| Method | Path | Description |
|--------|------|-------------|
| GET | /person/account/person/employees/{employeeId}/information | username and emailAddress of the connected account |

### wageprojection
| Method | Path | Description |
|--------|------|-------------|
| GET | /wageprojection/cladata/{collectiveLaborAgreementId} | Wage projection Collective labor agreements defaults |
| GET | /wageprojection/collectivelaboragreements | List of collective labor agreements (CLA) |

### rdwservices
| Method | Path | Description |
|--------|------|-------------|
| GET | /rdwservices/additionaltaxliability | Acquire the additional tax liability by the license plate number (company car) |

### achmeainsurancecontracts
| Method | Path | Description |
|--------|------|-------------|
| GET | /achmeainsurancecontracts | list of insurance contracts |
| GET | /achmeainsurancecontracts/{achmeaInsuranceContractId}/insuredwagecalculationpercentages | list of wage percentages for an insurance contract |

### qwoater
| Method | Path | Description |
|--------|------|-------------|
| GET | /qwoater/employers | List of employers using Qwoater |

### user
| Method | Path | Description |
|--------|------|-------------|
| GET | /user | Get current user |
| GET | /user/{userId} | Basic properties of a user |
| PUT | /user/{userId} | Edit current user |
| GET | /user/photo | Photo of an user |
| POST | /user/photo | Post user photo |
| DELETE | /user/photo | Delete user photo |

### globalfilter
| Method | Path | Description |
|--------|------|-------------|
| GET | /globalfilter/user/filtersettings/{employerId} | Get user filter settings |
| PUT | /globalfilter/user/filtersettings/{employerId} | Edit the user filter settings |

### locationservices
| Method | Path | Description |
|--------|------|-------------|
| GET | /locationservices/address | Acquire the address for a combination of `postalCode` and `houseNumber` |

### address
| Method | Path | Description |
|--------|------|-------------|
| GET | /address/search | Search for an address |

### route
| Method | Path | Description |
|--------|------|-------------|
| GET | /route/calculate | Calculates the distance for a given route |

### aowDate
| Method | Path | Description |
|--------|------|-------------|
| GET | /aowDate | Acquire the AOW date |

### chamberofcommerce
| Method | Path | Description |
|--------|------|-------------|
| GET | /chamberofcommerce/{chamberOfCommerceNumber}/companyinformation | Acquire company information |

### datanewbusiness
| Method | Path | Description |
|--------|------|-------------|
| GET | /datanewbusiness/token | Get Data New Business token |
| GET | /datanewbusiness/functions | Get a list of functions |

### applications
| Method | Path | Description |
|--------|------|-------------|
| GET | /applications/{applicationId}/authorizations | Authorizations for the application |
| GET | /applications/{applicationId}/logo | Download the application logo |

### applicationset
| Method | Path | Description |
|--------|------|-------------|
| GET | /applicationset/providers/employers/{employerId}/applicationsets | List of applicationsets for an employer |
| POST | /applicationset/providers/employers/{employerId}/applicationsets | Create an applicationset for an employer |
| PUT | /applicationset/providers/employers/applicationsets/{applicationSetId} | Edit the details of an applicationset |
| DELETE | /applicationset/providers/employers/applicationsets/{applicationSetId} | Delete a specific applicationset |
| GET | /applicationset/providers/{providerId}/applicationsets | List of applicationsets for a provider |
| POST | /applicationset/providers/{providerId}/applicationsets | Create an applicationset for a provider |
| PUT | /applicationset/providers/applicationsets/{applicationSetId} | Edit the details of an applicationset |
| DELETE | /applicationset/providers/applicationsets/{applicationSetId} | Delete a specific applicationset |
| GET | /applicationset/users/{userId}/applicationsets | List of applicationsets for a user |
| POST | /applicationset/users/{userId}/applicationsets | Create an applicationset for a user |
| PUT | /applicationset/users/applicationsets/{applicationSetId} | Edit the details of an applicationset for a user |
| DELETE | /applicationset/users/applicationsets/{applicationSetId} | Delete a specific applicationset for a user |
| GET | /applicationset/applicationsets/general | List of applicationsets provided by the Loket application |

### provider
| Method | Path | Description |
|--------|------|-------------|
| GET | /provider/providers/{providerId}/employers/modules | List modules per employer for all employers of the provider |
| GET | /provider/providers/{providerId}/payrollAdministrations/YearEndStatements | List of year-end statements for all payroll administrations of the provider |
| GET | /provider/providers/{providerId}/payrollAdministrations/Payslips | List of payslips per type for all payroll administrations of the provider |
| GET | /provider/providers/{providerId}/payrollAdministrations/employmentTurnover | List of employment turnover per payroll administration for the provider |

### payrolltaxreturn
| Method | Path | Description |
|--------|------|-------------|
| GET | /payrolltaxreturn/providers/employers/payrolladministrations/payrolltaxreturns/{payrollTaxReturnId}/report | Download the overview report of a payroll tax return |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all absences?" -> GET /v2/providers/employers/employees/{employeeId}/absences
- "Create a absence?" -> POST /v2/providers/employers/employees/{employeeId}/absences
- "List all overview?" -> GET /v2/providers/employers/employees/{employeeId}/absences/overview
- "Get absence details?" -> GET /v2/providers/employers/employees/absences/{absenceId}
- "Update a absence?" -> PUT /v2/providers/employers/employees/absences/{absenceId}
- "Delete a absence?" -> DELETE /v2/providers/employers/employees/absences/{absenceId}
- "List all absenceprogress?" -> GET /v2/providers/employers/employees/absences/{absenceId}/absenceprogress
- "Create a absenceprogress?" -> POST /v2/providers/employers/employees/absences/{absenceId}/absenceprogress
- "Get absenceprogress details?" -> GET /v2/providers/employers/employees/absences/absenceprogress/{absenceProgressId}
- "Update a absenceprogress?" -> PUT /v2/providers/employers/employees/absences/absenceprogress/{absenceProgressId}
- "Delete a absenceprogress?" -> DELETE /v2/providers/employers/employees/absences/absenceprogress/{absenceProgressId}
- "List all absencecontactHistory?" -> GET /v2/providers/employers/employees/absences/{absenceId}/absencecontactHistory
- "Create a absencecontactHistory?" -> POST /v2/providers/employers/employees/absences/{absenceId}/absencecontactHistory
- "Get absencecontactHistory details?" -> GET /v2/providers/employers/employees/absences/absencecontactHistory/{absencecontactHistoryId}
- "Update a absencecontactHistory?" -> PUT /v2/providers/employers/employees/absences/absencecontactHistory/{absencecontactHistoryId}
- "Delete a absencecontactHistory?" -> DELETE /v2/providers/employers/employees/absences/absencecontactHistory/{absencecontactHistoryId}
- "List all data?" -> GET /v2/providers/employers/{employerId}/employees/absences/statistics/data
- "List all administrations?" -> GET /v2/providers/employers/{employerId}/administrations
- "List all administrations?" -> GET /v2/providers/employers/administrations
- "List all payrolladministrations?" -> GET /v2/providers/employers/{employerId}/payrolladministrations
- "Create a payrolladministration?" -> POST /v2/providers/employers/{employerId}/payrolladministrations
- "Get payrolladministration details?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}
- "List all configurations?" -> GET /v2/providers/employers/{employerId}/payrolladministrations/configurations
- "List all configurations?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/configurations
- "List all automaticpayrollconfiguration?" -> GET /automaticpayroll/payrolladministrations/{payrollAdministrationId}/automaticpayrollconfiguration
- "List all automaticpayrolldates?" -> GET /automaticpayroll/payrolladministrations/years/{yearId}/automaticpayrolldates
- "Create a automaticpayrolldate?" -> POST /automaticpayroll/payrolladministrations/years/{yearId}/automaticpayrolldates
- "Partially update a automaticpayrolldate?" -> PATCH /automaticpayroll/payrolladministrations/years/automaticpayrolldates/{automaticPayrollDateId}
- "Delete a automaticpayrolldate?" -> DELETE /automaticpayroll/payrolladministrations/years/automaticpayrolldates/{automaticPayrollDateId}
- "List all authorizationmodel?" -> GET /authorizationmodel
- "List all nonpayrolladministrations?" -> GET /v2/providers/employers/{employerId}/nonpayrolladministrations
- "Create a nonpayrolladministration?" -> POST /v2/providers/employers/{employerId}/nonpayrolladministrations
- "Get nonpayrolladministration details?" -> GET /v2/providers/employers/nonpayrolladministrations/{nonPayrollAdministrationId}
- "Update a nonpayrolladministration?" -> PUT /v2/providers/employers/nonpayrolladministrations/{nonPayrollAdministrationId}
- "List all availablepayrollcomponentsets?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/availablepayrollcomponentsets
- "List all payrollcomponentsets?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollcomponentsets
- "Create a payrollcomponentset?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollcomponentsets
- "Get payrollcomponentset details?" -> GET /v2/providers/employers/payrolladministrations/payrollcomponentsets/{payrollComponentSetId}
- "Update a payrollcomponentset?" -> PUT /v2/providers/employers/payrolladministrations/payrollcomponentsets/{payrollComponentSetId}
- "Delete a payrollcomponentset?" -> DELETE /v2/providers/employers/payrolladministrations/payrollcomponentsets/{payrollComponentSetId}
- "List all payrollcomponentsets?" -> GET /v2/providers/{providerId}/payrollcomponentsets
- "Create a payrollcomponentset?" -> POST /v2/providers/{providerId}/payrollcomponentsets
- "Get payrollcomponentset details?" -> GET /v2/providers/payrollcomponentsets/{payrollComponentSetId}
- "Update a payrollcomponentset?" -> PUT /v2/providers/payrollcomponentsets/{payrollComponentSetId}
- "Delete a payrollcomponentset?" -> DELETE /v2/providers/payrollcomponentsets/{payrollComponentSetId}
- "Get year details?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollcomponents/year/{year}
- "Get year details?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/employmentfunds/year/{year}
- "Get year details?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/abpfunds/year/{year}
- "List all collectiveactions?" -> GET /users/collectiveactions
- "Get collectiveaction details?" -> GET /users/collectiveactions/{collectiveActionId}
- "List all employmentActualMasterDataReport?" -> GET /v2/providers/employers/{employerId}/employmentActualMasterDataReport
- "List all employmentMasterDataReport?" -> GET /v2/providers/employers/{employerId}/employmentMasterDataReport
- "List all fiscalCompanyCarReport?" -> GET /v2/providers/employers/{employerId}/fiscalCompanyCarReport
- "List all annualpayrolltaxreturnreport?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/annualpayrolltaxreturnreport
- "List all annualwagesheetreport?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/annualwagesheetreport
- "List all annualpawwdeclarationreport?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/annualpawwdeclarationreport
- "List all payrolladministrationsettingsreport?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrolladministrationsettingsreport
- "List all accumulationsandbalancesreport?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/accumulationsandbalancesreport
- "List all accumulatedbasicjournalresultsreport?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/accumulatedbasicjournalresultsreport
- "List all deviatingpremiumswab?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/deviatingpremiumswab
- "List all attachmentsofearningsreport?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/attachmentsofearningsreport
- "List all accumulatedjournalrunresultsreport"?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/accumulatedjournalrunresultsreport"
- "List all payrollPeriodDataReport?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollPeriodDataReport
- "List all PayrollAuditReport"?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/PayrollAuditReport"
- "List all employmentActualMasterDataReport?" -> GET /v2/providers/employers/employees/employments/{employmentId}/employmentActualMasterDataReport
- "List all employmentMasterDataReport?" -> GET /v2/providers/employers/employees/employments/{employmentId}/employmentMasterDataReport
- "List all payrollperioddata?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollPeriods/{payrollPeriodId}/payrollperioddata
- "Create a smartpaste?" -> POST /payrollcomponent/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollPeriods/{payrollPeriodId}/payrollperioddata/smartpaste
- "Get smartpaste details?" -> GET /payrollcomponent/providers/employers/payrolladministrations/payrollPeriods/payrollperioddata/smartpaste/{smartPasteId}
- "Create a payrollperioddata"?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/import/payrollperioddata"
- "Create a payrollperioddata"?" -> POST /v2/providers/employers/payrolladministrations/import/payrollperioddata"
- "List all workflowtriggers?" -> GET /v2/providers/employers/{employerId}/workflowtriggers
- "Get workflowtemplate details?" -> GET /v2/providers/employers/workflowtriggers/workflowtemplates/{workflowTemplateId}
- "Update a workflowtemplate?" -> PUT /v2/providers/employers/workflowtriggers/workflowtemplates/{workflowTemplateId}
- "Delete a workflowtemplate?" -> DELETE /v2/providers/employers/workflowtriggers/workflowtemplates/{workflowTemplateId}
- "Create a workflowtemplate?" -> POST /v2/providers/employers/{employerId}/workflowtriggers/{workflowTriggerId}/workflowtemplates
- "List all workflowtriggermappings?" -> GET /v2/providers/employers/{employerId}/workflowtriggermappings
- "Create a workflowtriggermapping?" -> POST /v2/providers/employers/{employerId}/workflowtriggermappings
- "Get workflowtriggermapping details?" -> GET /v2/providers/employers/workflowtriggermappings/{workflowTriggerMappingId}
- "Update a workflowtriggermapping?" -> PUT /v2/providers/employers/workflowtriggermappings/{workflowTriggerMappingId}
- "Delete a workflowtriggermapping?" -> DELETE /v2/providers/employers/workflowtriggermappings/{workflowTriggerMappingId}
- "Create a changeaddressrequest?" -> POST /v2/providers/employers/employees/{employeeId}/changeaddressrequest
- "Create a changecontactinformationrequest?" -> POST /v2/providers/employers/employees/{employeeId}/changecontactinformationrequest
- "Create a InitiateChangeAddress?" -> POST /v2/providers/employers/employees/{employeeId}/workflow/InitiateChangeAddress
- "Create a InitiateChangeContactInformation?" -> POST /v2/providers/employers/employees/{employeeId}/workflow/InitiateChangeContactInformation
- "Create a InitiateChangePersonalInformation?" -> POST /v2/providers/employers/employees/{employeeId}/workflow/InitiateChangePersonalInformation
- "Create a InitiateManagePartner?" -> POST /v2/providers/employers/employees/{employeeId}/workflow/InitiateManagePartners
- "Create a InitiateManageContact?" -> POST /v2/providers/employers/employees/{employeeId}/workflow/InitiateManageContacts
- "Create a InitiateDeclaration?" -> POST /v2/providers/employers/employees/employments/{employmentId}/workflow/InitiateDeclaration
- "Create a InitiateChangeIban?" -> POST /v2/providers/employers/employees/employments/{employmentId}/workflow/InitiateChangeIban
- "Create a InitiateLeaveRequest?" -> POST /v2/providers/employers/employees/employments/{employmentId}/workflow/InitiateLeaveRequest
- "Create a WithdrawLeaveRequest?" -> POST /v2/providers/employers/employees/employments/leaveRequests/{leaveRequestId}/workflow/WithdrawLeaveRequest
- "Create a initiatecontractextension?" -> POST /v2/providers/employers/employees/employments/{employmentId}/workflows/initiatecontractextension
- "Create a initiateterminateemployment?" -> POST /v2/providers/employers/employees/employments/{employmentId}/workflows/initiateterminateemployment
- "List all attachment?" -> GET /v2/providers/employers/employees/employments/workflow/{workflowId}/attachment
- "Create a attachment?" -> POST /v2/providers/employers/employees/employments/workflow/{workflowId}/attachment
- "List all withattachment?" -> GET /qwoatermicroservice/providers/employers/employees/employments/{employmentId}/workflows/withattachment
- "List all withattachment?" -> GET /qwoatermicroservice/providers/employers/{employerId}/employees/employments/workflows/withattachment
- "List all assignedworkflows?" -> GET /v2/providers/employers/{employerId}/assignedworkflows
- "List all initiatedworkflows?" -> GET /users/initiatedworkflows
- "List all workflows?" -> GET /v2/providers/employers/{employerId}/workflows
- "Get workflow details?" -> GET /v2/providers/employers/workflows/{workflowId}
- "Create a transition?" -> POST /v2/providers/employers/workflows/{workflowId}/transition
- "List all workflows?" -> GET /v2/providers/employers/employees/employments/{employmentId}/workflows
- "List all workflowprogress?" -> GET /v2/providers/employers/workflows/{workflowId}/workflowprogress
- "List all employees?" -> GET /v2/providers/employers/{employerId}/employees
- "Get employee details?" -> GET /v2/providers/employers/employees/{employeeId}
- "Update a employee?" -> PUT /v2/providers/employers/employees/{employeeId}
- "Partially update a employee?" -> PATCH /v2/providers/employers/employees/{employeeId}
- "List all contacts?" -> GET /v2/providers/employers/employees/{employeeId}/contacts
- "Create a contact?" -> POST /v2/providers/employers/employees/{employeeId}/contacts
- "Get contact details?" -> GET /v2/providers/employers/employees/contacts/{contactId}
- "Update a contact?" -> PUT /v2/providers/employers/employees/contacts/{contactId}
- "Delete a contact?" -> DELETE /v2/providers/employers/employees/contacts/{contactId}
- "List all children?" -> GET /v2/providers/employers/employees/{employeeId}/children
- "Create a children?" -> POST /v2/providers/employers/employees/{employeeId}/children
- "Get children details?" -> GET /v2/providers/employers/employees/children/{childId}
- "Update a children?" -> PUT /v2/providers/employers/employees/children/{childId}
- "Delete a children?" -> DELETE /v2/providers/employers/employees/children/{childId}
- "List all occupationaldisabilities?" -> GET /v2/providers/employers/employees/{employeeId}/occupationaldisabilities
- "List all partners?" -> GET /v2/providers/employers/employees/{employeeId}/partners
- "Create a partner?" -> POST /v2/providers/employers/employees/{employeeId}/partners
- "Get partner details?" -> GET /v2/providers/employers/employees/partners/{partnerId}
- "Update a partner?" -> PUT /v2/providers/employers/employees/partners/{partnerId}
- "Delete a partner?" -> DELETE /v2/providers/employers/employees/partners/{partnerId}
- "List all citizenservicenumber?" -> GET /v2/providers/employers/employees/{employeeId}/citizenservicenumber
- "List all photo?" -> GET /v2/providers/employers/employees/{employeeId}/photo
- "Create a photo?" -> POST /v2/providers/employers/employees/{employeeId}/photo
- "Get photo details?" -> GET /v2/providers/employers/employees/{employeeId}/photo/{version}
- "Create a employee?" -> POST /v2/providers/employers/{employerId}/employee
- "List all customfields?" -> GET /v2/providers/employers/employees/{employeeId}/customfields
- "Create a customfield?" -> POST /v2/providers/employers/employees/{employeeId}/customfields
- "Get customfield details?" -> GET /v2/providers/employers/employees/customfields/{employeeCustomFieldId}
- "Update a customfield?" -> PUT /v2/providers/employers/employees/customfields/{employeeCustomFieldId}
- "Delete a customfield?" -> DELETE /v2/providers/employers/employees/customfields/{employeeCustomFieldId}
- "List all employers?" -> GET /v2/providers/employers
- "List all minimized?" -> GET /v2/providers/employers/minimized
- "Create a employer?" -> POST /v2/providers/{providerId}/employers
- "List all minimized?" -> GET /v2/providers/{providerId}/employers/minimized
- "List all informationForWizard?" -> GET /v2/providers/{providerId}/employers/informationForWizard
- "Get employer details?" -> GET /v2/providers/employers/{employerId}
- "Update a employer?" -> PUT /v2/providers/employers/{employerId}
- "List all childEmployers?" -> GET /v2/providers/employers/{employerId}/childEmployers
- "List all functions?" -> GET /v2/providers/employers/{employerId}/functions
- "Create a function?" -> POST /v2/providers/employers/{employerId}/functions
- "Get function details?" -> GET /v2/providers/employers/functions/{functionId}
- "Update a function?" -> PUT /v2/providers/employers/functions/{functionId}
- "List all departments?" -> GET /v2/providers/employers/{employerId}/departments
- "Create a department?" -> POST /v2/providers/employers/{employerId}/departments
- "Get department details?" -> GET /v2/providers/employers/departments/{departmentId}
- "Update a department?" -> PUT /v2/providers/employers/departments/{departmentId}
- "List all useraccessibledepartments?" -> GET /v2/providers/employers/{employerId}/useraccessibledepartments
- "List all logo?" -> GET /v2/providers/employers/{employerId}/logo
- "Create a logo?" -> POST /v2/providers/employers/{employerId}/logo
- "Get logo details?" -> GET /v2/providers/employers/{employerId}/logo/{version}
- "List all providerlogo?" -> GET /v2/providers/employers/{employerId}/providerlogo
- "Get providerlogo details?" -> GET /v2/providers/employers/{employerId}/providerlogo/{version}
- "List all dashboard?" -> GET /v2/providers/employers/{employerId}/dashboard
- "List all customfields?" -> GET /v2/providers/employers/{employerId}/customfields
- "Create a customfield?" -> POST /v2/providers/employers/{employerId}/customfields
- "Get customfield details?" -> GET /v2/providers/employers/customfields/{customFieldId}
- "Update a customfield?" -> PUT /v2/providers/employers/customfields/{customFieldId}
- "Delete a customfield?" -> DELETE /v2/providers/employers/customfields/{customFieldId}
- "List all educationtypes?" -> GET /v2/providers/employers/{employerId}/educationtypes
- "Create a educationtype?" -> POST /v2/providers/employers/{employerId}/educationtypes
- "Get educationtype details?" -> GET /v2/providers/employers/educationtypes/{educationTypeId}
- "Update a educationtype?" -> PUT /v2/providers/employers/educationtypes/{educationTypeId}
- "Delete a educationtype?" -> DELETE /v2/providers/employers/educationtypes/{educationTypeId}
- "List all educationfurtherindications?" -> GET /v2/providers/employers/{employerId}/educationfurtherindications
- "Create a educationfurtherindication?" -> POST /v2/providers/employers/{employerId}/educationfurtherindications
- "Get educationfurtherindication details?" -> GET /v2/providers/employers/educationfurtherindications/{educationFurtherIndicationId}
- "Update a educationfurtherindication?" -> PUT /v2/providers/employers/educationfurtherindications/{educationFurtherIndicationId}
- "Delete a educationfurtherindication?" -> DELETE /v2/providers/employers/educationfurtherindications/{educationFurtherIndicationId}
- "List all contractcodes?" -> GET /v2/providers/employers/{employerId}/contractcodes
- "Create a contractcode?" -> POST /v2/providers/employers/{employerId}/contractcodes
- "Get contractcode details?" -> GET /v2/providers/employers/contractcodes/{contractCodeId}
- "Update a contractcode?" -> PUT /v2/providers/employers/contractcodes/{contractCodeId}
- "Delete a contractcode?" -> DELETE /v2/providers/employers/contractcodes/{contractCodeId}
- "List all benefitinkindtypes?" -> GET /v2/providers/employers/{employerId}/benefitinkindtypes
- "Create a benefitinkindtype?" -> POST /v2/providers/employers/{employerId}/benefitinkindtypes
- "Get benefitinkindtype details?" -> GET /v2/providers/employers/benefitinkindtypes/{benefitInKindTypeId}
- "Update a benefitinkindtype?" -> PUT /v2/providers/employers/benefitinkindtypes/{benefitInKindTypeId}
- "Delete a benefitinkindtype?" -> DELETE /v2/providers/employers/benefitinkindtypes/{benefitInKindTypeId}
- "List all customholidays?" -> GET /v2/providers/employers/{employerId}/customholidays
- "Create a customholiday?" -> POST /v2/providers/employers/{employerId}/customholidays
- "Get customholiday details?" -> GET /v2/providers/employers/customholidays/{customHolidayId}
- "Update a customholiday?" -> PUT /v2/providers/employers/customholidays/{customHolidayId}
- "Delete a customholiday?" -> DELETE /v2/providers/employers/customholidays/{customHolidayId}
- "List all billableitems?" -> GET /billing/providers/employers/{employerId}/billableitems
- "List all nationalholidays?" -> GET /v2/providers/employers/{employerId}/nationalholidays
- "Get nationalholiday details?" -> GET /v2/providers/employers/{employerId}/nationalholidays/{nationalHolidayId}
- "Update a nationalholiday?" -> PUT /v2/providers/employers/{employerId}/nationalholidays/{nationalHolidayId}
- "List all configuration?" -> GET /v2/providers/employers/{employerId}/configuration
- "List all distributionunits?" -> GET /v2/providers/employers/{employerId}/distributionunits
- "Create a distributionunit?" -> POST /v2/providers/employers/{employerId}/distributionunits
- "Get distributionunit details?" -> GET /v2/providers/employers/distributionunits/{distributionUnitId}
- "Update a distributionunit?" -> PUT /v2/providers/employers/distributionunits/{distributionUnitId}
- "Create a requestyeartransition?" -> POST /year/providers/employers/payrolladministrations/years/{yearId}/requestyeartransition
- "List all selfservice?" -> GET /v2/providers/employers/{employerId}/conceptemployees/selfservice
- "List all selfservice?" -> GET /v2/providers/employers/conceptemployees/{conceptEmployeeId}/selfservice
- "List all selfservice?" -> GET /v2/providers/employers/{employerId}/employees/selfservice
- "List all selfservice?" -> GET /v2/providers/employers/employees/{employeeId}/selfservice
- "List all migration?" -> GET /v2/providers/employers/{employerId}/employees/selfservice/migration
- "List all information?" -> GET /person/account/person/employees/{employeeId}/information
- "List all essaccessstatus?" -> GET /v2/providers/employers/{employerId}/employees/essaccessstatus
- "List all authorizations?" -> GET /v2/providers/employers/{employerId}/authorizations
- "List all authorizations?" -> GET /v2/providers/{providerId}/authorizations
- "List all modules?" -> GET /v2/providers/employers/{employerId}/modules
- "List all modules?" -> GET /v2/providers/{providerId}/modules
- "List all conceptemployees?" -> GET /v2/providers/employers/{employerId}/conceptemployees
- "Create a conceptemployee?" -> POST /v2/providers/employers/{employerId}/conceptemployees
- "Get minimized details?" -> GET /v2/providers/employers/conceptemployees/minimized/{conceptEmployeeId}
- "Update a minimized?" -> PUT /v2/providers/employers/conceptemployees/minimized/{conceptEmployeeId}
- "Get conceptemployee details?" -> GET /v2/providers/employers/conceptemployees/{conceptEmployeeId}
- "Update a conceptemployee?" -> PUT /v2/providers/employers/conceptemployees/{conceptEmployeeId}
- "Delete a conceptemployee?" -> DELETE /v2/providers/employers/conceptemployees/{conceptEmployeeId}
- "List all citizenservicenumber?" -> GET /v2/providers/employers/conceptemployees/{conceptEmployeeId}/citizenservicenumber
- "Get paygrade details?" -> GET /v2/providers/employers/conceptemployees/metadata/payrollAdministration/{payrollAdministrationId}/payScale/{payscaleKey}/paygrade/{paygradeKey}
- "List all preboardingtrajectory?" -> GET /v2/providers/employers/conceptemployees/{conceptEmployeeId}/preboardingtrajectory
- "Create a preboardingtrajectory?" -> POST /v2/providers/employers/conceptemployees/{conceptEmployeeId}/preboardingtrajectory
- "List all actualpaygradeamounts?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/employees/employments/actualpaygradeamounts
- "Create a initiate?" -> POST /v2/providers/employers/conceptemployees/{conceptEmployeeId}/assessment/initiate
- "List all assessments?" -> GET /v2/providers/employers/{employerId}/assessments
- "List all contactpersons?" -> GET /v2/providers/employers/conceptemployees/{conceptEmployeeId}/contactpersons
- "Create a contactperson?" -> POST /v2/providers/employers/conceptemployees/{conceptEmployeeId}/contactpersons
- "List all metadata?" -> GET /v2/providers/employers/conceptemployees/{conceptEmployeeId}/contactpersons/metadata
- "Update a contactperson?" -> PUT /v2/providers/employers/conceptemployees/contactpersons/{contactPersonId}
- "Delete a contactperson?" -> DELETE /v2/providers/employers/conceptemployees/contactpersons/{contactPersonId}
- "List all metadata?" -> GET /v2/providers/employers/conceptemployees/contactpersons/{contactPersonId}/metadata
- "List all notifications?" -> GET /v2/providers/employers/{employerId}/notifications
- "List all notifications?" -> GET /v2/providers/employers/notifications
- "List all summary?" -> GET /v2/providers/employers/notifications/summary
- "Get notification details?" -> GET /v2/providers/employers/notifications/{notificationId}
- "List all announcements?" -> GET /v2/providers/employers/{employerId}/announcements
- "List all announcements?" -> GET /v2/providers/employers/announcements
- "List all summary?" -> GET /v2/providers/employers/announcements/summary
- "Get announcement details?" -> GET /v2/providers/employers/announcements/{announcementId}
- "List all employments?" -> GET /v2/providers/employers/{employerId}/employees/employments
- "List all minimized?" -> GET /v2/providers/employers/{employerId}/employees/employments/minimized
- "List all comprehensive?" -> GET /v2/providers/employers/{employerId}/employees/employments/comprehensive
- "List all employments?" -> GET /v2/providers/employers/employees/{employeeId}/employments
- "Create a employment?" -> POST /v2/providers/employers/employees/{employeeId}/employments
- "Get employment details?" -> GET /v2/providers/employers/employees/employments/{employmentId}
- "Update a employment?" -> PUT /v2/providers/employers/employees/employments/{employmentId}
- "Partially update a employment?" -> PATCH /v2/providers/employers/employees/employments/{employmentId}
- "Delete a employment?" -> DELETE /v2/providers/employers/employees/employments/{employmentId}
- "Create a transitioncompensation?" -> POST /v2/providers/employers/employees/employments/{employmentId}/transitioncompensation
- "List all deleteinformation?" -> GET /v2/providers/employers/employees/employments/{employmentId}/deleteinformation
- "List all payrollperioddata?" -> GET /v2/providers/employers/employees/employments/{employmentId}/payrollperioddata
- "Create a payrollperioddata?" -> POST /v2/providers/employers/employees/employments/{employmentId}/payrollperioddata
- "Get payrollperioddata details?" -> GET /v2/providers/employers/employees/employments/payrollperioddata/{payrollperioddataId}
- "Update a payrollperioddata?" -> PUT /v2/providers/employers/employees/employments/payrollperioddata/{payrollperioddataId}
- "Delete a payrollperioddata?" -> DELETE /v2/providers/employers/employees/employments/payrollperioddata/{payrollperioddataId}
- "List all benefitsanddeductions?" -> GET /v2/providers/employers/employees/employments/{employmentId}/benefitsanddeductions
- "Create a benefitsanddeduction?" -> POST /v2/providers/employers/employees/employments/{employmentId}/benefitsanddeductions
- "Get benefitsAndDeduction details?" -> GET /v2/providers/employers/employees/employments/benefitsAndDeductions/{benefitsanddeductionsId}
- "Update a benefitsAndDeduction?" -> PUT /v2/providers/employers/employees/employments/benefitsAndDeductions/{benefitsanddeductionsId}
- "Delete a benefitsAndDeduction?" -> DELETE /v2/providers/employers/employees/employments/benefitsAndDeductions/{benefitsanddeductionsId}
- "List all benefitsanddeductions"?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/import/benefitsanddeductions"
- "Create a benefitsanddeductions"?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/import/benefitsanddeductions"
- "Create a benefitsanddeduction?" -> POST /v2/providers/employers/{employerId}/employees/employments/benefitsanddeductions
- "Create a wageprojection?" -> POST /v2/providers/employers/employees/employments/{employmentId}/wageprojection
- "Create a basedOnDefaultClaConfiguration?" -> POST /v2/providers/employers/employees/employments/{employmentId}/wageprojection/basedOnDefaultClaConfiguration
- "Get cladata details?" -> GET /wageprojection/cladata/{collectiveLaborAgreementId}
- "List all collectivelaboragreements?" -> GET /wageprojection/collectivelaboragreements
- "List all educations?" -> GET /v2/providers/employers/employees/{employeeId}/educations
- "Create a education?" -> POST /v2/providers/employers/employees/{employeeId}/educations
- "Get education details?" -> GET /v2/providers/employers/employees/educations/{employeeEducationId}
- "Update a education?" -> PUT /v2/providers/employers/employees/educations/{employeeEducationId}
- "Delete a education?" -> DELETE /v2/providers/employers/employees/educations/{employeeEducationId}
- "List all declarations?" -> GET /v2/providers/employers/employees/employments/{employmentId}/declarations
- "Create a declaration?" -> POST /v2/providers/employers/employees/employments/{employmentId}/declarations
- "Get declaration details?" -> GET /v2/providers/employers/employees/employments/declarations/{declarationId}
- "Update a declaration?" -> PUT /v2/providers/employers/employees/employments/declarations/{declarationId}
- "Delete a declaration?" -> DELETE /v2/providers/employers/employees/employments/declarations/{declarationId}
- "List all audittrail?" -> GET /v2/providers/employers/employees/employments/declarations/{declarationId}/audittrail
- "Create a receipt?" -> POST /v2/providers/employers/employees/employments/{employmentId}/declarations/analyze/receipt
- "List all wages?" -> GET /v2/providers/employers/employees/employments/{employmentId}/wages
- "Create a wage?" -> POST /v2/providers/employers/employees/employments/{employmentId}/wages
- "Get wage details?" -> GET /v2/providers/employers/employees/employments/wages/{wageId}
- "Update a wage?" -> PUT /v2/providers/employers/employees/employments/wages/{wageId}
- "Delete a wage?" -> DELETE /v2/providers/employers/employees/employments/wages/{wageId}
- "List all wage"?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/import/wage"
- "Create a wage"?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/import/wage"
- "Create a wage?" -> POST /v2/providers/employers/{employerId}/employees/employments/wages
- "List all minimumwage?" -> GET /v2/providers/employers/employees/employments/{employmentId}/minimumwage
- "List all costperhour?" -> GET /v2/providers/employers/employees/employments/{employmentId}/costperhour
- "Create a costperhour?" -> POST /v2/providers/employers/employees/employments/{employmentId}/costperhour
- "Get costperhour details?" -> GET /v2/providers/employers/employees/employments/costperhour/{costPerHourId}
- "Update a costperhour?" -> PUT /v2/providers/employers/employees/employments/costperhour/{costPerHourId}
- "Delete a costperhour?" -> DELETE /v2/providers/employers/employees/employments/costperhour/{costPerHourId}
- "List all workinghours?" -> GET /v2/providers/employers/employees/employments/{employmentId}/workinghours
- "Create a workinghour?" -> POST /v2/providers/employers/employees/employments/{employmentId}/workinghours
- "Get workinghour details?" -> GET /v2/providers/employers/employees/employments/workinghours/{workinghoursId}
- "Update a workinghour?" -> PUT /v2/providers/employers/employees/employments/workinghours/{workinghoursId}
- "Delete a workinghour?" -> DELETE /v2/providers/employers/employees/employments/workinghours/{workinghoursId}
- "List all organizationalentities?" -> GET /v2/providers/employers/employees/employments/{employmentId}/organizationalentities
- "Create a organizationalentity?" -> POST /v2/providers/employers/employees/employments/{employmentId}/organizationalentities
- "Get organizationalentity details?" -> GET /v2/providers/employers/employees/employments/organizationalentities/{organizationalEntityId}
- "Update a organizationalentity?" -> PUT /v2/providers/employers/employees/employments/organizationalentities/{organizationalEntityId}
- "Delete a organizationalentity?" -> DELETE /v2/providers/employers/employees/employments/organizationalentities/{organizationalEntityId}
- "List all paymentinformationsepa?" -> GET /v2/providers/employers/employees/employments/{employmentId}/paymentinformationsepa
- "Create a paymentinformationsepa?" -> POST /v2/providers/employers/employees/employments/{employmentId}/paymentinformationsepa
- "Get paymentinformationsepa details?" -> GET /v2/providers/employers/employees/employments/paymentinformationsepa/{paymentInformationSepaId}
- "Update a paymentinformationsepa?" -> PUT /v2/providers/employers/employees/employments/paymentinformationsepa/{paymentInformationSepaId}
- "Delete a paymentinformationsepa?" -> DELETE /v2/providers/employers/employees/employments/paymentinformationsepa/{paymentInformationSepaId}
- "List all paymentinformationsepaseparatepayments?" -> GET /v2/providers/employers/employees/employments/{employmentId}/paymentinformationsepaseparatepayments
- "Create a paymentinformationsepaseparatepayment?" -> POST /v2/providers/employers/employees/employments/{employmentId}/paymentinformationsepaseparatepayments
- "Get paymentinformationsepaseparatepayment details?" -> GET /v2/providers/employers/employees/employments/paymentinformationsepaseparatepayments/{paymentInformationSepaSeparatePaymentId}
- "Update a paymentinformationsepaseparatepayment?" -> PUT /v2/providers/employers/employees/employments/paymentinformationsepaseparatepayments/{paymentInformationSepaSeparatePaymentId}
- "Delete a paymentinformationsepaseparatepayment?" -> DELETE /v2/providers/employers/employees/employments/paymentinformationsepaseparatepayments/{paymentInformationSepaSeparatePaymentId}
- "List all paymentinformationnonsepa?" -> GET /v2/providers/employers/employees/employments/{employmentId}/paymentinformationnonsepa
- "Create a paymentinformationnonsepa?" -> POST /v2/providers/employers/employees/employments/{employmentId}/paymentinformationnonsepa
- "Get paymentinformationnonsepa details?" -> GET /v2/providers/employers/employees/employments/paymentinformationnonsepa/{paymentInformationNonSepaId}
- "Update a paymentinformationnonsepa?" -> PUT /v2/providers/employers/employees/employments/paymentinformationnonsepa/{paymentInformationNonSepaId}
- "Delete a paymentinformationnonsepa?" -> DELETE /v2/providers/employers/employees/employments/paymentinformationnonsepa/{paymentInformationNonSepaId}
- "List all attachmentsofearnings?" -> GET /v2/providers/employers/employees/employments/{employmentId}/attachmentsofearnings
- "Create a attachmentsofearning?" -> POST /v2/providers/employers/employees/employments/{employmentId}/attachmentsofearnings
- "Get attachmentsofearning details?" -> GET /v2/providers/employers/employees/employments/attachmentsofearnings/{attachmentOfEarningsId}
- "Update a attachmentsofearning?" -> PUT /v2/providers/employers/employees/employments/attachmentsofearnings/{attachmentOfEarningsId}
- "Delete a attachmentsofearning?" -> DELETE /v2/providers/employers/employees/employments/attachmentsofearnings/{attachmentOfEarningsId}
- "List all protectedearnings?" -> GET /v2/providers/employers/employees/employments/{employmentId}/protectedearnings
- "Create a protectedearning?" -> POST /v2/providers/employers/employees/employments/{employmentId}/protectedearnings
- "Get protectedearning details?" -> GET /v2/providers/employers/employees/employments/protectedearnings/{protectedEarningsId}
- "Update a protectedearning?" -> PUT /v2/providers/employers/employees/employments/protectedearnings/{protectedEarningsId}
- "Delete a protectedearning?" -> DELETE /v2/providers/employers/employees/employments/protectedearnings/{protectedEarningsId}
- "List all fiscalproperties?" -> GET /v2/providers/employers/employees/employments/{employmentId}/fiscalproperties
- "Create a fiscalproperty?" -> POST /v2/providers/employers/employees/employments/{employmentId}/fiscalproperties
- "Get fiscalproperty details?" -> GET /v2/providers/employers/employees/employments/fiscalproperties/{fiscalPropertiesId}
- "Update a fiscalproperty?" -> PUT /v2/providers/employers/employees/employments/fiscalproperties/{fiscalPropertiesId}
- "Delete a fiscalproperty?" -> DELETE /v2/providers/employers/employees/employments/fiscalproperties/{fiscalPropertiesId}
- "List all calculatedannualsalary?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/employees/employments/calculatedannualsalary
- "Create a fiscalproperty?" -> POST /v2/providers/employers/{employerId}/employees/employments/fiscalproperties
- "List all fiscalcompanycars?" -> GET /v2/providers/employers/employees/employments/{employmentId}/fiscalcompanycars
- "Create a fiscalcompanycar?" -> POST /v2/providers/employers/employees/employments/{employmentId}/fiscalcompanycars
- "Get fiscalcompanycar details?" -> GET /v2/providers/employers/employees/employments/fiscalcompanycars/{fiscalCompanyCarId}
- "Update a fiscalcompanycar?" -> PUT /v2/providers/employers/employees/employments/fiscalcompanycars/{fiscalCompanyCarId}
- "Delete a fiscalcompanycar?" -> DELETE /v2/providers/employers/employees/employments/fiscalcompanycars/{fiscalCompanyCarId}
- "Create a fiscalcompanycar?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/import/fiscalcompanycars
- "List all companycars?" -> GET /v2/providers/employers/employees/employments/{employmentId}/companycars
- "Create a companycar?" -> POST /v2/providers/employers/employees/employments/{employmentId}/companycars
- "Get companycar details?" -> GET /v2/providers/employers/employees/employments/companycars/{companyCarId}
- "Update a companycar?" -> PUT /v2/providers/employers/employees/employments/companycars/{companyCarId}
- "Delete a companycar?" -> DELETE /v2/providers/employers/employees/employments/companycars/{companyCarId}
- "List all additionaltaxliability?" -> GET /rdwservices/additionaltaxliability
- "List all employmentfunds?" -> GET /v2/providers/employers/employees/employments/{employmentId}/employmentfunds
- "Create a employmentfund?" -> POST /v2/providers/employers/employees/employments/{employmentId}/employmentfunds
- "Get employmentfund details?" -> GET /v2/providers/employers/employees/employments/employmentfunds/{employmentFundId}
- "Update a employmentfund?" -> PUT /v2/providers/employers/employees/employments/employmentfunds/{employmentFundId}
- "Delete a employmentfund?" -> DELETE /v2/providers/employers/employees/employments/employmentfunds/{employmentFundId}
- "List all abpfunds?" -> GET /v2/providers/employers/employees/employments/{employmentId}/abpfunds
- "Create a abpfund?" -> POST /v2/providers/employers/employees/employments/{employmentId}/abpfunds
- "Get abpfund details?" -> GET /v2/providers/employers/employees/employments/abpfunds/{abpFundId}
- "Update a abpfund?" -> PUT /v2/providers/employers/employees/employments/abpfunds/{abpFundId}
- "Delete a abpfund?" -> DELETE /v2/providers/employers/employees/employments/abpfunds/{abpFundId}
- "Create a employmentfund?" -> POST /v2/providers/employers/{employerId}/employees/employments/employmentfunds
- "Create a abpfund?" -> POST /v2/providers/employers/{employerId}/employees/employments/abpfunds
- "List all basesforemploymentfundcalculation?" -> GET /v2/providers/employers/employees/employments/{employmentId}/basesforemploymentfundcalculation
- "Create a basesforemploymentfundcalculation?" -> POST /v2/providers/employers/employees/employments/{employmentId}/basesforemploymentfundcalculation
- "Get basesforemploymentfundcalculation details?" -> GET /v2/providers/employers/employees/employments/basesforemploymentfundcalculation/{baseforemploymentfundcalculationId}
- "Update a basesforemploymentfundcalculation?" -> PUT /v2/providers/employers/employees/employments/basesforemploymentfundcalculation/{baseforemploymentfundcalculationId}
- "Delete a basesforemploymentfundcalculation?" -> DELETE /v2/providers/employers/employees/employments/basesforemploymentfundcalculation/{baseforemploymentfundcalculationId}
- "List all basesforcalculation?" -> GET /v2/providers/employers/employees/employments/{employmentId}/basesforcalculation
- "Create a basesforcalculation?" -> POST /v2/providers/employers/employees/employments/{employmentId}/basesforcalculation
- "Get basesforcalculation details?" -> GET /v2/providers/employers/employees/employments/basesforcalculation/{baseforcalculationId}
- "Update a basesforcalculation?" -> PUT /v2/providers/employers/employees/employments/basesforcalculation/{baseforcalculationId}
- "Delete a basesforcalculation?" -> DELETE /v2/providers/employers/employees/employments/basesforcalculation/{baseforcalculationId}
- "Create a basesforcalculation?" -> POST /v2/providers/employers/{employerId}/employees/employments/basesforcalculation
- "List all deviatingawfcontributions?" -> GET /v2/providers/employers/employees/employments/{employmentId}/deviatingawfcontributions
- "Create a deviatingawfcontribution?" -> POST /v2/providers/employers/employees/employments/{employmentId}/deviatingawfcontributions
- "Get deviatingawfcontribution details?" -> GET /v2/providers/employers/employees/employments/deviatingawfcontributions/{deviatingAwfContributionId}
- "Update a deviatingawfcontribution?" -> PUT /v2/providers/employers/employees/employments/deviatingawfcontributions/{deviatingAwfContributionId}
- "Delete a deviatingawfcontribution?" -> DELETE /v2/providers/employers/employees/employments/deviatingawfcontributions/{deviatingAwfContributionId}
- "List all pensionbenefits?" -> GET /v2/providers/employers/employees/employments/{employmentId}/pensionbenefits
- "Create a pensionbenefit?" -> POST /v2/providers/employers/employees/employments/{employmentId}/pensionbenefits
- "Get pensionbenefit details?" -> GET /v2/providers/employers/employees/employments/pensionbenefits/{pensionBenefitId}
- "Update a pensionbenefit?" -> PUT /v2/providers/employers/employees/employments/pensionbenefits/{pensionBenefitId}
- "Delete a pensionbenefit?" -> DELETE /v2/providers/employers/employees/employments/pensionbenefits/{pensionBenefitId}
- "List all deviatinghourlywages?" -> GET /v2/providers/employers/employees/employments/{employmentId}/deviatinghourlywages
- "Create a deviatinghourlywage?" -> POST /v2/providers/employers/employees/employments/{employmentId}/deviatinghourlywages
- "Get deviatinghourlywage details?" -> GET /v2/providers/employers/employees/employments/deviatinghourlywages/{deviatingHourlyWageId}
- "Update a deviatinghourlywage?" -> PUT /v2/providers/employers/employees/employments/deviatinghourlywages/{deviatingHourlyWageId}
- "Delete a deviatinghourlywage?" -> DELETE /v2/providers/employers/employees/employments/deviatinghourlywages/{deviatingHourlyWageId}
- "List all benefitsInKind?" -> GET /v2/providers/employers/employees/employments/{employmentId}/benefitsInKind
- "Create a benefitsInKind?" -> POST /v2/providers/employers/employees/employments/{employmentId}/benefitsInKind
- "Get benefitsinkind details?" -> GET /v2/providers/employers/employees/employments/benefitsinkind/{benefitInKindId}
- "Update a benefitsinkind?" -> PUT /v2/providers/employers/employees/employments/benefitsinkind/{benefitInKindId}
- "Delete a benefitsinkind?" -> DELETE /v2/providers/employers/employees/employments/benefitsinkind/{benefitInKindId}
- "List all customnotifications?" -> GET /v2/providers/employers/employees/employments/{employmentId}/customnotifications
- "Create a customnotification?" -> POST /v2/providers/employers/employees/employments/{employmentId}/customnotifications
- "Get customnotification details?" -> GET /v2/providers/employers/employees/employments/customnotifications/{customNotificationId}
- "Update a customnotification?" -> PUT /v2/providers/employers/employees/employments/customnotifications/{customNotificationId}
- "Delete a customnotification?" -> DELETE /v2/providers/employers/employees/employments/customnotifications/{customNotificationId}
- "List all customfields?" -> GET /v2/providers/employers/employees/employments/{employmentId}/customfields
- "Create a customfield?" -> POST /v2/providers/employers/employees/employments/{employmentId}/customfields
- "Get customfield details?" -> GET /v2/providers/employers/employees/employments/customfields/{employmentCustomFieldId}
- "Update a customfield?" -> PUT /v2/providers/employers/employees/employments/customfields/{employmentCustomFieldId}
- "Delete a customfield?" -> DELETE /v2/providers/employers/employees/employments/customfields/{employmentCustomFieldId}
- "List all otherPayrollVariables?" -> GET /v2/providers/employers/employees/employments/{employmentId}/otherPayrollVariables
- "Create a otherPayrollVariable?" -> POST /v2/providers/employers/employees/employments/{employmentId}/otherPayrollVariables
- "Get otherPayrollVariable details?" -> GET /v2/providers/employers/employees/employments/otherPayrollVariables/{otherPayrollVariablesId}
- "Update a otherPayrollVariable?" -> PUT /v2/providers/employers/employees/employments/otherPayrollVariables/{otherPayrollVariablesId}
- "Delete a otherPayrollVariable?" -> DELETE /v2/providers/employers/employees/employments/otherPayrollVariables/{otherPayrollVariablesId}
- "List all socialsecurityconfigurations?" -> GET /v2/providers/employers/employees/employments/{employmentId}/socialsecurityconfigurations
- "Create a socialsecurityconfiguration?" -> POST /v2/providers/employers/employees/employments/{employmentId}/socialsecurityconfigurations
- "Get socialsecurityconfiguration details?" -> GET /v2/providers/employers/employees/employments/socialsecurityconfigurations/{socialSecurityConfigurationId}
- "Update a socialsecurityconfiguration?" -> PUT /v2/providers/employers/employees/employments/socialsecurityconfigurations/{socialSecurityConfigurationId}
- "Delete a socialsecurityconfiguration?" -> DELETE /v2/providers/employers/employees/employments/socialsecurityconfigurations/{socialSecurityConfigurationId}
- "List all socialsecuritybenefits?" -> GET /v2/providers/employers/employees/employments/{employmentId}/socialsecuritybenefits
- "Create a socialsecuritybenefit?" -> POST /v2/providers/employers/employees/employments/{employmentId}/socialsecuritybenefits
- "Get socialsecuritybenefit details?" -> GET /v2/providers/employers/employees/employments/socialsecuritybenefits/{socialSecurityBenefitId}
- "Update a socialsecuritybenefit?" -> PUT /v2/providers/employers/employees/employments/socialsecuritybenefits/{socialSecurityBenefitId}
- "Delete a socialsecuritybenefit?" -> DELETE /v2/providers/employers/employees/employments/socialsecuritybenefits/{socialSecurityBenefitId}
- "List all healthcareinsuranceactconfigurations?" -> GET /v2/providers/employers/employees/employments/{employmentId}/healthcareinsuranceactconfigurations
- "Create a healthcareinsuranceactconfiguration?" -> POST /v2/providers/employers/employees/employments/{employmentId}/healthcareinsuranceactconfigurations
- "Get healthcareinsuranceactconfiguration details?" -> GET /v2/providers/employers/employees/employments/healthcareinsuranceactconfigurations/{healthcareInsuranceActConfigurationId}
- "Update a healthcareinsuranceactconfiguration?" -> PUT /v2/providers/employers/employees/employments/healthcareinsuranceactconfigurations/{healthcareInsuranceActConfigurationId}
- "Delete a healthcareinsuranceactconfiguration?" -> DELETE /v2/providers/employers/employees/employments/healthcareinsuranceactconfigurations/{healthcareInsuranceActConfigurationId}
- "List all wachtgeld?" -> GET /v2/providers/employers/employees/employments/{employmentId}/wachtgeld
- "Create a wachtgeld?" -> POST /v2/providers/employers/employees/employments/{employmentId}/wachtgeld
- "Get wachtgeld details?" -> GET /v2/providers/employers/employees/employments/wachtgeld/{wachtgeldId}
- "Update a wachtgeld?" -> PUT /v2/providers/employers/employees/employments/wachtgeld/{wachtgeldId}
- "Delete a wachtgeld?" -> DELETE /v2/providers/employers/employees/employments/wachtgeld/{wachtgeldId}
- "List all contacts?" -> GET /v2/providers/employers/{employerId}/employees/contacts
- "List all children?" -> GET /v2/providers/employers/{employerId}/employees/children
- "List all citizenservicenumbers?" -> GET /v2/providers/employers/{employerId}/employees/citizenservicenumbers
- "List all customfields?" -> GET /v2/providers/employers/{employerId}/employees/customfields
- "List all partners?" -> GET /v2/providers/employers/{employerId}/employees/partners
- "List all customfields?" -> GET /v2/providers/employers/{employerId}/employees/employments/customfields
- "List all paymentinformationsepa?" -> GET /v2/providers/employers/{employerId}/employees/employments/paymentinformationsepa
- "List all actualorganizationalentities?" -> GET /v2/providers/employers/{employerId}/actualorganizationalentities
- "List all actualwages?" -> GET /v2/providers/employers/{employerId}/actualwages
- "List all actualworkinghours?" -> GET /v2/providers/employers/{employerId}/actualworkinghours
- "List all actualbenefitsanddeductions?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualbenefitsanddeductions
- "List all actualemploymentfunds?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualemploymentfunds
- "List all actualabpfunds?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualabpfunds
- "List all actualfiscalproperties?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualfiscalproperties
- "List all actualhealthcareinsuranceactconfigurations?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualhealthcareinsuranceactconfigurations
- "List all actualsocialsecurityconfigurations?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualsocialsecurityconfigurations
- "List all actualsocialsecuritybenefits?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualsocialsecuritybenefits
- "List all actualdeviatingawfcontributions?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualdeviatingawfcontributions
- "List all actualbenefitsinkind?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualbenefitsinkind
- "List all actualcompanycars?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualcompanycars
- "List all actualfiscalcompanycars?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualfiscalcompanycars
- "List all actualjournalallocations?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualjournalallocations
- "List all actualbasesforcalculation?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualbasesforcalculation
- "List all actualotherpayrollvariables?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualotherpayrollvariables
- "List all actualpaymentinformationnonsepa?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualpaymentinformationnonsepa
- "List all actualbasesforemploymentfundcalculation?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualbasesforemploymentfundcalculation
- "List all actualpensionbenefits?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualpensionbenefits
- "List all actualdeviatinghourlywages?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualdeviatinghourlywages
- "List all actualcostperhour?" -> GET /v2/providers/employers/{employerId}/employees/employments/actualcostperhour
- "List all achmeainsurancecontracts?" -> GET /achmeainsurancecontracts
- "List all insuredwagecalculationpercentages?" -> GET /achmeainsurancecontracts/{achmeaInsuranceContractId}/insuredwagecalculationpercentages
- "List all benifyurl?" -> GET /v2/providers/employers/employees/{employeeId}/benifyurl
- "List all yourcampus?" -> GET /users/yourcampus
- "List all employers?" -> GET /qwoater/employers
- "List all leavePolicies?" -> GET /v2/providers/employers/{employerId}/leavePolicies
- "Create a leavePolicy?" -> POST /v2/providers/employers/{employerId}/leavePolicies
- "Get leavePolicy details?" -> GET /v2/providers/employers/leavePolicies/{leavePolicyId}
- "Update a leavePolicy?" -> PUT /v2/providers/employers/leavePolicies/{leavePolicyId}
- "Delete a leavePolicy?" -> DELETE /v2/providers/employers/leavePolicies/{leavePolicyId}
- "List all agebasedleave?" -> GET /v2/providers/employers/leavePolicies/{leavePolicyId}/agebasedleave
- "Create a agebasedleave?" -> POST /v2/providers/employers/leavePolicies/{leavePolicyId}/agebasedleave
- "Get agebasedleave details?" -> GET /v2/providers/employers/leavePolicies/agebasedleave/{ageBasedLeaveId}
- "Update a agebasedleave?" -> PUT /v2/providers/employers/leavePolicies/agebasedleave/{ageBasedLeaveId}
- "Delete a agebasedleave?" -> DELETE /v2/providers/employers/leavePolicies/agebasedleave/{ageBasedLeaveId}
- "List all yearsofservicebasedleave?" -> GET /v2/providers/employers/leavePolicies/{leavePolicyId}/yearsofservicebasedleave
- "Create a yearsofservicebasedleave?" -> POST /v2/providers/employers/leavePolicies/{leavePolicyId}/yearsofservicebasedleave
- "Get yearsofservicebasedleave details?" -> GET /v2/providers/employers/leavePolicies/yearsofservicebasedleave/{yearsOfServiceBasedLeaveId}
- "Update a yearsofservicebasedleave?" -> PUT /v2/providers/employers/leavePolicies/yearsofservicebasedleave/{yearsOfServiceBasedLeaveId}
- "Delete a yearsofservicebasedleave?" -> DELETE /v2/providers/employers/leavePolicies/yearsofservicebasedleave/{yearsOfServiceBasedLeaveId}
- "List all wagebasedleave?" -> GET /v2/providers/employers/leavePolicies/{leavePolicyId}/wagebasedleave
- "Create a wagebasedleave?" -> POST /v2/providers/employers/leavePolicies/{leavePolicyId}/wagebasedleave
- "Get wagebasedleave details?" -> GET /v2/providers/employers/leavePolicies/wagebasedleave/{wageBasedLeaveId}
- "Update a wagebasedleave?" -> PUT /v2/providers/employers/leavePolicies/wagebasedleave/{wageBasedLeaveId}
- "Delete a wagebasedleave?" -> DELETE /v2/providers/employers/leavePolicies/wagebasedleave/{wageBasedLeaveId}
- "List all employments?" -> GET /v2/providers/employers/leavepolicies/{leavePolicyId}/employments
- "List all accrual?" -> GET /v2/providers/employers/leavepolicies/{leavePolicyId}/employments/leave/accrual
- "List all accrual"?" -> GET /v2/providers/employers/leavepolicies/{leavePolicyId}/employments/{employmentId}/leave/accrual"
- "List all entitlement?" -> GET /v2/providers/employers/leavepolicies/{leavePolicyId}/employments/leave/entitlement
- "List all entitlement"?" -> GET /v2/providers/employers/leavepolicies/{leavePolicyId}/employments/{employmentId}/leave/entitlement"
- "List all leavePolicies?" -> GET /v2/providers/{providerId}/leavePolicies
- "Create a leavePolicy?" -> POST /v2/providers/{providerId}/leavePolicies
- "Get leavePolicy details?" -> GET /v2/providers/leavePolicies/{leavePolicyId}
- "Update a leavePolicy?" -> PUT /v2/providers/leavePolicies/{leavePolicyId}
- "Delete a leavePolicy?" -> DELETE /v2/providers/leavePolicies/{leavePolicyId}
- "List all agebasedleave?" -> GET /v2/providers/leavePolicies/{leavePolicyId}/agebasedleave
- "Create a agebasedleave?" -> POST /v2/providers/leavePolicies/{leavePolicyId}/agebasedleave
- "Get agebasedleave details?" -> GET /v2/providers/leavePolicies/agebasedleave/{ageBasedLeaveId}
- "Update a agebasedleave?" -> PUT /v2/providers/leavePolicies/agebasedleave/{ageBasedLeaveId}
- "Delete a agebasedleave?" -> DELETE /v2/providers/leavePolicies/agebasedleave/{ageBasedLeaveId}
- "List all yearsofservicebasedleave?" -> GET /v2/providers/leavePolicies/{leavePolicyId}/yearsofservicebasedleave
- "Create a yearsofservicebasedleave?" -> POST /v2/providers/leavePolicies/{leavePolicyId}/yearsofservicebasedleave
- "Get yearsofservicebasedleave details?" -> GET /v2/providers/leavePolicies/yearsofservicebasedleave/{yearsOfServiceBasedLeaveId}
- "Update a yearsofservicebasedleave?" -> PUT /v2/providers/leavePolicies/yearsofservicebasedleave/{yearsOfServiceBasedLeaveId}
- "Delete a yearsofservicebasedleave?" -> DELETE /v2/providers/leavePolicies/yearsofservicebasedleave/{yearsOfServiceBasedLeaveId}
- "List all wagebasedleave?" -> GET /v2/providers/leavePolicies/{leavePolicyId}/wagebasedleave
- "Create a wagebasedleave?" -> POST /v2/providers/leavePolicies/{leavePolicyId}/wagebasedleave
- "Get agebasedleave details?" -> GET /v2/providers/leavePolicies/agebasedleave/{wageBasedLeaveId}
- "Update a agebasedleave?" -> PUT /v2/providers/leavePolicies/agebasedleave/{wageBasedLeaveId}
- "Delete a agebasedleave?" -> DELETE /v2/providers/leavePolicies/agebasedleave/{wageBasedLeaveId}
- "List all leavetypes?" -> GET /v2/providers/employers/{employerId}/leavetypes
- "Get leavetype details?" -> GET /v2/providers/employers/{employerId}/leavetypes/{leaveTypeId}
- "Update a leavetype?" -> PUT /v2/providers/employers/{employerId}/leavetypes/{leaveTypeId}
- "List all leaverequests?" -> GET /v2/providers/employers/{employerId}/employees/employments/leaverequests
- "List all currentlyAvailableUnits?" -> GET /v2/providers/employers/employees/employments/leaverequests/currentlyAvailableUnits
- "List all leave?" -> GET /v2/providers/employers/employees/employments/{employmentId}/leave
- "Create a leave?" -> POST /v2/providers/employers/employees/employments/{employmentId}/leave
- "Get leave details?" -> GET /v2/providers/employers/employees/employments/leave/{leaveId}
- "Update a leave?" -> PUT /v2/providers/employers/employees/employments/leave/{leaveId}
- "Delete a leave?" -> DELETE /v2/providers/employers/employees/employments/leave/{leaveId}
- "List all metadata?" -> GET /v2/providers/employers/employees/employments/{employmentId}/leave/metadata
- "List all defaults?" -> GET /v2/providers/employers/employees/employments/{employmentId}/leave/defaults
- "List all metadata?" -> GET /v2/providers/employers/employees/employments/leave/{leaveId}/metadata
- "List all proposedleavehours?" -> GET /v2/providers/employers/employees/employments/{employmentId}/leave/proposedleavehours
- "List all proposedleavehours?" -> GET /v2/providers/employers/{employerId}/leave/proposedleavehours
- "Get overview details?" -> GET /v2/providers/employers/employees/employments/{employmentId}/leave/overview/{year}
- "List all leaverequests?" -> GET /v2/providers/employers/employees/employments/{employmentId}/leaverequests
- "Create a leaverequest?" -> POST /v2/providers/employers/employees/employments/{employmentId}/leaverequests
- "Get leaverequest details?" -> GET /v2/providers/employers/employees/employments/leaverequests/{leaveRequestId}
- "Update a leaverequest?" -> PUT /v2/providers/employers/employees/employments/leaverequests/{leaveRequestId}
- "List all leavebalances?" -> GET /v2/providers/employers/employees/employments/{employmentId}/leavebalances
- "List all leavebalances?" -> GET /v2/providers/employers/{employerId}/leavebalances
- "List all worth?" -> GET /v2/providers/employers/{employerId}/leavebalances/worth
- "List all grouped?" -> GET /v2/providers/employers/{employerId}/leavebalances/grouped
- "List all leavepolicies?" -> GET /v2/providers/employers/employees/employments/{employmentId}/leavepolicies
- "List all leave"?" -> GET /v2/providers/employers/{employerId}/import/leave"
- "Create a leave"?" -> POST /v2/providers/employers/{employerId}/import/leave"
- "Create a leave?" -> POST /v2/providers/employers/{employerId}/leave
- "List all payrollprocessoverview?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollprocessoverview
- "List all payrollruns?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollruns
- "Get payrollrun details?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}
- "Partially update a payrollrun?" -> PATCH /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}
- "Create a periodreadyforpayroll?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/periodreadyforpayroll
- "List all payslips?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/payslips
- "List all defaultset?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/defaultset
- "List all paymentoverviews?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/paymentoverviews
- "List all wagesheets?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/wagesheets
- "List all sepafiles?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/sepafiles
- "List all sepahashes?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/sepahashes
- "Get sepafile details?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/sepafiles/{sepafileId}
- "List all totalsepafile?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/totalsepafile
- "List all runoverviews?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/runoverviews
- "List all payrollcontrolregister?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/payrollcontrolregister
- "List all journalentriesperdistributionunitoverviews?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/journalentriesperdistributionunitoverviews
- "List all errorsandwarnings?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/errorsandwarnings
- "List all nonsepafile?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/nonsepafile
- "List all payrollPeriodDataAuditTrail?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollPeriodDataAuditTrail
- "List all employmentPayrollDataAuditTrail?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/employmentPayrollDataAuditTrail
- "List all payrollperiods?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollperiods
- "List all minimized?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollperiods/minimized
- "List all payrollresults?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollperiods/{payrollPeriodId}/payrollresults
- "List all compare?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollperiods/compare
- "List all data?" -> GET /v2/providers/employers/{employerId}/payrollresults/statistics/data
- "Get payrollcomponent details?" -> GET /v2/providers/employers/{employerId}/employees/employments/payrollperiods/payrollcomponents/{payrollComponent}
- "List all compare?" -> GET /v2/providers/employers/payrolladministrations/payrollperiods/payrollresults/compare
- "List all results?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/results
- "List all BalanceSheet?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/BalanceSheet
- "List all payrollresults?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollresults
- "List all payrollresults"?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/payrollresults"
- "List all payrollresults"?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollperiods/payrollresults"
- "List all grouped"?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollperiods/payrollresults/grouped"
- "List all providers?" -> GET /providers
- "List all logo?" -> GET /v2/providers/{providerId}/logo
- "Get logo details?" -> GET /v2/providers/{providerId}/logo/{version}
- "List all contactinformation?" -> GET /v2/providers/{providerId}/contactinformation
- "List all billableitems?" -> GET /billing/providers/{providerId}/billableitems
- "List all dashboard?" -> GET /v2/providers/{providerId}/dashboard
- "List all logos?" -> GET /v2/providers/{providerId}/logos
- "Create a logo?" -> POST /v2/providers/{providerId}/logos
- "Get logo details?" -> GET /v2/providers/logos/{logoId}
- "Update a logo?" -> PUT /v2/providers/logos/{logoId}
- "Delete a logo?" -> DELETE /v2/providers/logos/{logoId}
- "List all logo?" -> GET /v2/providers/logos/{logoId}/logo
- "List all configuration?" -> GET /v2/providers/{providerId}/configuration
- "List all payslip?" -> GET /v2/providers/{providerId}/configuration/payslip
- "List all logo?" -> GET /v2/providers/{providerId}/configuration/payslip/logo
- "Create a logo?" -> POST /v2/providers/{providerId}/configuration/payslip/logo
- "List all notificationsettings?" -> GET /v2/providers/{providerId}/notificationsettings
- "List all groupclassifications?" -> GET /v2/providers/{providerId}/groupclassifications
- "Create a groupclassification?" -> POST /v2/providers/{providerId}/groupclassifications
- "Update a groupclassification?" -> PUT /v2/providers/groupclassifications/{groupClassificationId}
- "Delete a groupclassification?" -> DELETE /v2/providers/groupclassifications/{groupClassificationId}
- "List all workrelatedcostsutilization?" -> GET /v2/providers/employers/payrolladministrations/workrelatedcostsutilization
- "List all usage?" -> GET /qwoatermicroservice/providers/employers/dossier/usage
- "List all usage?" -> GET /qwoatermicroservice/providers/employers/signature/usage
- "List all authorizationsets?" -> GET /v2/providers/{providerId}/authorizationsets
- "Create a authorizationset?" -> POST /v2/providers/{providerId}/authorizationsets
- "Get authorizationset details?" -> GET /v2/providers/authorizationsets/{authorizationSetId}
- "Update a authorizationset?" -> PUT /v2/providers/authorizationsets/{authorizationSetId}
- "Delete a authorizationset?" -> DELETE /v2/providers/authorizationsets/{authorizationSetId}
- "List all modulesets?" -> GET /v2/providers/{providerId}/modulesets
- "Create a moduleset?" -> POST /v2/providers/{providerId}/modulesets
- "Get moduleset details?" -> GET /v2/providers/modulesets/{moduleSetId}
- "Partially update a moduleset?" -> PATCH /v2/providers/modulesets/{moduleSetId}
- "Delete a moduleset?" -> DELETE /v2/providers/modulesets/{moduleSetId}
- "List all moduleset?" -> GET /v2/providers/employers/{employerId}/moduleset
- "List all notificationsets?" -> GET /v2/providers/{providerId}/notificationsets
- "Create a notificationset?" -> POST /v2/providers/{providerId}/notificationsets
- "Get notificationset details?" -> GET /v2/providers/notificationsets/{notificationSetId}
- "Partially update a notificationset?" -> PATCH /v2/providers/notificationsets/{notificationSetId}
- "Delete a notificationset?" -> DELETE /v2/providers/notificationsets/{notificationSetId}
- "List all status?" -> GET /v2/providers/employers/payrolladministrations/payrollperiods/{payrollPeriodId}/payrollruns/status
- "List all status"?" -> GET /v2/providers/employers/payrolladministrations/payrollperiods/{payrollPeriodId}/payrolltaxreturns/status"
- "List all status?" -> GET /v2/providers/employers/payrolladministrations/payrollperiods/{payrollPeriodId}/pensiondeclaration/status
- "List all status?" -> GET /year/providers/employers/payrolladministrations/years/{year}/status
- "List all journalruns?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/journalruns
- "Get journalrun details?" -> GET /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}
- "Partially update a journalrun?" -> PATCH /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}
- "Create a initiate?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/journalruns/initiate
- "Create a undo?" -> POST /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/undo
- "Create a recalculate?" -> POST /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/journalruns/recalculate
- "List all results?" -> GET /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/results
- "List all cumulativeresults?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/journalruns/cumulativeresults
- "List all report?" -> GET /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/report
- "List all runoverview?" -> GET /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/runoverview
- "List all runoverviewperemployment?" -> GET /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/runoverviewperemployment
- "List all exportAuditTrail?" -> GET /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/exportAuditTrail
- "List all errors?" -> GET /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/errors
- "Create a send?" -> POST /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/send
- "Create a download?" -> POST /v2/providers/employers/payrolladministrations/journalruns/{journalrunId}/download
- "List all journalConfigurations?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/journalConfigurations
- "Create a journalConfiguration?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/journalConfigurations
- "Get journalConfiguration details?" -> GET /v2/providers/employers/payrolladministrations/journalConfigurations/{journalConfigurationId}
- "Update a journalConfiguration?" -> PUT /v2/providers/employers/payrolladministrations/journalConfigurations/{journalConfigurationId}
- "Delete a journalConfiguration?" -> DELETE /v2/providers/employers/payrolladministrations/journalConfigurations/{journalConfigurationId}
- "List all journalApplication?" -> GET /v2/providers/employers/payrolladministrations/journalConfigurations/{journalConfigurationId}/journalApplication
- "Create a journalApplication?" -> POST /v2/providers/employers/payrolladministrations/journalConfigurations/{journalConfigurationId}/journalApplication
- "List all journalProfiles?" -> GET /v2/providers/{providerId}/journalProfiles
- "Create a journalProfile?" -> POST /v2/providers/{providerId}/journalProfiles
- "Get journalProfile details?" -> GET /v2/providers/journalProfiles/{journalProfileId}
- "Update a journalProfile?" -> PUT /v2/providers/journalProfiles/{journalProfileId}
- "Delete a journalProfile?" -> DELETE /v2/providers/journalProfiles/{journalProfileId}
- "List all ledgerAccounts?" -> GET /v2/providers/journalProfiles/{journalProfileId}/ledgerAccounts
- "Create a ledgerAccount?" -> POST /v2/providers/journalProfiles/{journalProfileId}/ledgerAccounts
- "Get ledgerAccount details?" -> GET /v2/providers/journalProfiles/ledgerAccounts/{ledgerAccountId}
- "Partially update a ledgerAccount?" -> PATCH /v2/providers/journalProfiles/ledgerAccounts/{ledgerAccountId}
- "Delete a ledgerAccount?" -> DELETE /v2/providers/journalProfiles/ledgerAccounts/{ledgerAccountId}
- "List all ledgerAccountToPayrollComponentLinks"?" -> GET /v2/providers/journalProfiles/{journalProfileId}/ledgerAccountToPayrollComponentLinks"
- "Create a ledgerAccountToPayrollComponentLinks"?" -> POST /v2/providers/journalProfiles/{journalProfileId}/ledgerAccountToPayrollComponentLinks"
- "Get ledgerAccountToPayrollComponentLink details?" -> GET /v2/providers/journalProfiles/ledgerAccountToPayrollComponentLinks/{ledgerAccountToPayrollComponentLinkId}
- "Partially update a ledgerAccountToPayrollComponentLink?" -> PATCH /v2/providers/journalProfiles/ledgerAccountToPayrollComponentLinks/{ledgerAccountToPayrollComponentLinkId}
- "Delete a ledgerAccountToPayrollComponentLink?" -> DELETE /v2/providers/journalProfiles/ledgerAccountToPayrollComponentLinks/{ledgerAccountToPayrollComponentLinkId}
- "List all costCenters?" -> GET /v2/providers/journalProfiles/{journalProfileId}/costCenters
- "Create a costCenter?" -> POST /v2/providers/journalProfiles/{journalProfileId}/costCenters
- "Get costCenter details?" -> GET /v2/providers/journalProfiles/costCenters/{costCenterId}
- "Partially update a costCenter?" -> PATCH /v2/providers/journalProfiles/costCenters/{costCenterId}
- "Delete a costCenter?" -> DELETE /v2/providers/journalProfiles/costCenters/{costCenterId}
- "List all costUnits?" -> GET /v2/providers/journalProfiles/{journalProfileId}/costUnits
- "Create a costUnit?" -> POST /v2/providers/journalProfiles/{journalProfileId}/costUnits
- "Get costUnit details?" -> GET /v2/providers/journalProfiles/costUnits/{costUnitId}
- "Partially update a costUnit?" -> PATCH /v2/providers/journalProfiles/costUnits/{costUnitId}
- "Delete a costUnit?" -> DELETE /v2/providers/journalProfiles/costUnits/{costUnitId}
- "List all CostCenterCostUnitMatrix?" -> GET /v2/providers/journalprofiles/{journalProfileId}/CostCenterCostUnitMatrix
- "List all journalProfiles?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/journalProfiles
- "Get journalProfile details?" -> GET /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}
- "Partially update a journalProfile?" -> PATCH /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}
- "List all ledgerAccounts?" -> GET /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/ledgerAccounts
- "Create a ledgerAccount?" -> POST /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/ledgerAccounts
- "Get ledgerAccount details?" -> GET /v2/providers/employers/payrolladministrations/journalProfiles/ledgerAccounts/{ledgerAccountId}
- "Partially update a ledgerAccount?" -> PATCH /v2/providers/employers/payrolladministrations/journalProfiles/ledgerAccounts/{ledgerAccountId}
- "Delete a ledgerAccount?" -> DELETE /v2/providers/employers/payrolladministrations/journalProfiles/ledgerAccounts/{ledgerAccountId}
- "List all ledgerAccountToPayrollComponentLinks?" -> GET /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/ledgerAccountToPayrollComponentLinks
- "Create a ledgerAccountToPayrollComponentLink?" -> POST /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/ledgerAccountToPayrollComponentLinks
- "List all metadata?" -> GET /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/ledgerAccountToPayrollComponentLinks/metadata
- "Get ledgerAccountToPayrollComponentLink details?" -> GET /v2/providers/employers/payrolladministrations/journalProfiles/ledgerAccountToPayrollComponentLinks/{ledgerAccountToPayrollComponentLinkId}
- "Partially update a ledgerAccountToPayrollComponentLink?" -> PATCH /v2/providers/employers/payrolladministrations/journalProfiles/ledgerAccountToPayrollComponentLinks/{ledgerAccountToPayrollComponentLinkId}
- "Delete a ledgerAccountToPayrollComponentLink?" -> DELETE /v2/providers/employers/payrolladministrations/journalProfiles/ledgerAccountToPayrollComponentLinks/{ledgerAccountToPayrollComponentLinkId}
- "List all costCenters?" -> GET /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/costCenters
- "Create a costCenter?" -> POST /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/costCenters
- "Get costCenter details?" -> GET /v2/providers/employers/payrolladministrations/journalProfiles/costCenters/{costCenterId}
- "Partially update a costCenter?" -> PATCH /v2/providers/employers/payrolladministrations/journalProfiles/costCenters/{costCenterId}
- "Delete a costCenter?" -> DELETE /v2/providers/employers/payrolladministrations/journalProfiles/costCenters/{costCenterId}
- "List all costUnits?" -> GET /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/costUnits
- "Create a costUnit?" -> POST /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/costUnits
- "Get costUnit details?" -> GET /v2/providers/employers/payrolladministrations/journalProfiles/costUnits/{costUnitId}
- "Partially update a costUnit?" -> PATCH /v2/providers/employers/payrolladministrations/journalProfiles/costUnits/{costUnitId}
- "Delete a costUnit?" -> DELETE /v2/providers/employers/payrolladministrations/journalProfiles/costUnits/{costUnitId}
- "List all CostCenterCostUnitMatrix?" -> GET /v2/providers/employers/payrolladministrations/journalProfiles/{journalProfileId}/CostCenterCostUnitMatrix
- "List all journalallocations?" -> GET /v2/providers/employers/employees/employments/{employmentId}/journalallocations
- "Create a journalallocation?" -> POST /v2/providers/employers/employees/employments/{employmentId}/journalallocations
- "Get journalallocation details?" -> GET /v2/providers/employers/employees/employments/journalallocations/{journalAllocationId}
- "Update a journalallocation?" -> PUT /v2/providers/employers/employees/employments/journalallocations/{journalAllocationId}
- "Delete a journalallocation?" -> DELETE /v2/providers/employers/employees/employments/journalallocations/{journalAllocationId}
- "List all user?" -> GET /user
- "Get user details?" -> GET /user/{userId}
- "Update a user?" -> PUT /user/{userId}
- "List all photo?" -> GET /user/photo
- "Create a photo?" -> POST /user/photo
- "Get filtersetting details?" -> GET /globalfilter/user/filtersettings/{employerId}
- "Update a filtersetting?" -> PUT /globalfilter/user/filtersettings/{employerId}
- "List all users?" -> GET /v2/providers/{providerId}/users
- "Create a user?" -> POST /v2/providers/{providerId}/users
- "Get user details?" -> GET /v2/providers/users/{userId}
- "Update a user?" -> PUT /v2/providers/users/{userId}
- "Delete a user?" -> DELETE /v2/providers/users/{userId}
- "Create a invite?" -> POST /v2/providers/{providerId}/users/invite
- "List all authorizations?" -> GET /v2/providers/users/{userId}/authorizations
- "List all authorizationSet?" -> GET /v2/providers/users/{userId}/authorizationSet
- "List all authorizationGroups?" -> GET /v2/providers/users/{userId}/authorizationGroups
- "List all clients?" -> GET /v2/providers/users/{userId}/clients
- "List all authorizationgroups?" -> GET /v2/providers/{providerId}/authorizationgroups
- "Create a authorizationgroup?" -> POST /v2/providers/{providerId}/authorizationgroups
- "Get authorizationgroup details?" -> GET /v2/providers/authorizationgroups/{authorizationGroupId}
- "Update a authorizationgroup?" -> PUT /v2/providers/authorizationgroups/{authorizationGroupId}
- "Delete a authorizationgroup?" -> DELETE /v2/providers/authorizationgroups/{authorizationGroupId}
- "List all authorizations?" -> GET /v2/providers/authorizationgroups/{authorizationGroupId}/authorizations
- "List all employers?" -> GET /v2/providers/authorizationgroups/{authorizationGroupId}/employers
- "List all users?" -> GET /v2/providers/authorizationgroups/{authorizationGroupId}/users
- "List all authorizationGroups?" -> GET /v2/providers/{providerId}/employers/{employerId}/authorizationGroups
- "List all integrations?" -> GET /users/integrations
- "List all integrations?" -> GET /v2/providers/employers/users/{userId}/integrations
- "Update a integration?" -> PUT /v2/providers/employers/users/{userId}/integrations/{applicationId}
- "Delete a integration?" -> DELETE /v2/providers/employers/users/{userId}/integrations/{applicationId}
- "List all logo?" -> GET /v2/providers/employers/users/{userId}/integrations/{applicationId}/logo
- "List all integrations?" -> GET /v2/providers/users/{userId}/integrations
- "Update a integration?" -> PUT /v2/providers/users/{userId}/integrations/{applicationId}
- "Delete a integration?" -> DELETE /v2/providers/users/{userId}/integrations/{applicationId}
- "List all logo?" -> GET /v2/providers/users/{userId}/integrations/{applicationId}/logo
- "List all clients?" -> GET /users/clients
- "List all clients?" -> GET /v2/providers/employers/users/{userId}/clients
- "List all connectedApplications?" -> GET /users/connectedApplications
- "Delete a connectedApplication?" -> DELETE /users/connectedApplications/{connectedApplicationId}
- "List all connectedApplications?" -> GET /v2/providers/users/{userId}/connectedApplications
- "Delete a connectedApplication?" -> DELETE /v2/providers/users/connectedApplications/{connectedApplicationId}
- "List all users?" -> GET /v2/providers/employers/{employerId}/users
- "Create a user?" -> POST /v2/providers/employers/{employerId}/users
- "Create a invite?" -> POST /v2/providers/employers/{employerId}/users/invite
- "Get user details?" -> GET /v2/providers/employers/users/{userId}
- "Update a user?" -> PUT /v2/providers/employers/users/{userId}
- "Delete a user?" -> DELETE /v2/providers/employers/users/{userId}
- "List all informationForDelete?" -> GET /v2/providers/employers/{employerId}/users/{userId}/informationForDelete
- "Delete a user?" -> DELETE /v2/providers/employers/{employerId}/users/{userId}
- "List all users?" -> GET /v2/providers/{providerId}/employers/users
- "List all employers?" -> GET /v2/providers/employers/users/{userId}/employers
- "List all departments?" -> GET /v2/providers/employers/{employerId}/users/departments
- "List all notificationsettings?" -> GET /v2/providers/employers/users/{userId}/notificationsettings
- "List all notificationset?" -> GET /v2/providers/employers/users/{userId}/notificationset
- "List all authorizations?" -> GET /v2/providers/employers/{employerId}/users/{userId}/authorizations
- "List all authorizationSet?" -> GET /v2/providers/employers/{employerId}/users/{userId}/authorizationSet
- "Create a link?" -> POST /v2/providers/employers/{employerId}/users/link
- "List all recommendedactions?" -> GET /v2/providers/employers/{employerId}/recommendedactions
- "List all employee?" -> GET /v2/providers/employers/{employerId}/users/{userId}/employee
- "List all userResponsibilities?" -> GET /v2/providers/{providerId}/userResponsibilities
- "Create a userResponsibility?" -> POST /v2/providers/{providerId}/userResponsibilities
- "Update a userResponsibility?" -> PUT /v2/providers/{providerId}/userResponsibilities/{userResponsibilityId}
- "List all userResponsibilities?" -> GET /v2/providers/employers/{employerId}/userResponsibilities
- "List all users?" -> GET /v2/providers/employers/{employerId}/userResponsibilities/{userResponsibilityId}/users
- "List all userResponsibilities?" -> GET /v2/providers/employers/{employerId}/users/{userId}/userResponsibilities
- "List all dashboardLicenses?" -> GET /v2/providers/employers/{employerId}/dashboardLicenses
- "List all externaltenants?" -> GET /v2/providers/{providerId}/externaltenants
- "List all externaltenants?" -> GET /v2/providers/employers/{employerId}/externaltenants
- "List all configuredexternaltenant?" -> GET /v2/providers/users/{providerUserId}/configuredexternaltenant
- "List all configuredexternaltenant?" -> GET /v2/providers/employers/users/{employerUserId}/configuredexternaltenant
- "List all payslips?" -> GET /v2/providers/employers/employees/employments/{employmentId}/payslips
- "Get payslip details?" -> GET /v2/providers/employers/employees/employments/{employmentId}/payslips/{year}
- "Get payslip details?" -> GET /v2/providers/employers/employees/employments/{employmentId}/payslips/{payrollrunId}
- "Get year details?" -> GET /v2/providers/employers/employees/employments/{employmentId}/payrollperiodresults/year/{year}
- "Get summary details?" -> GET /v2/providers/employers/employees/employments/{employmentId}/payslips/summary/{payrollPeriodId}
- "Get wagesheet details?" -> GET /v2/providers/employers/employees/employments/{employmentId}/wagesheet/{year}
- "List all yearendstatements?" -> GET /v2/providers/employers/employees/employments/{employmentId}/yearendstatements
- "Get yearendstatement details?" -> GET /v2/providers/employers/employees/employments/{employmentId}/yearendstatements/{year}
- "List all yearendstatements?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/yearendstatements
- "Get yearendstatement details?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/yearendstatements/{year}
- "List all payrolltaxreturns?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrolltaxreturns
- "List all overview?" -> GET /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}/overview
- "List all message?" -> GET /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}/message
- "List all sepafile?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrolltaxreturns/{payrolltaxreturnId}/sepafile
- "List all sepahash?" -> GET /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}/sepahash
- "Get payrolltaxreturn details?" -> GET /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}
- "List all ideal?" -> GET /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}/ideal
- "List all idealPaymentStatus?" -> GET /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}/idealPaymentStatus
- "List all report?" -> GET /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}/report
- "Create a sendresponsemessage?" -> POST /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}/sendresponsemessage
- "Partially update a payrolltaxreturn?" -> PATCH /v2/providers/employers/payrolladministrations/payrolltaxreturns/{messageReference}
- "Create a sendresponsemessagebymessagereference?" -> POST /v2/providers/employers/payrolladministrations/payrolltaxreturns/{messageReference}/sendresponsemessagebymessagereference
- "Create a initiate?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrolltaxreturns/initiate
- "Create a initiateForPreviousYear?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrolltaxreturns/initiateForPreviousYear
- "Create a initiateAnnual?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrolltaxreturns/initiateAnnual
- "Create a payrolltaxreturn?" -> POST /v2/providers/employers/payrolladministrations/payrollperiods/{payrollPeriodId}/payrolltaxreturns
- "Create a undo?" -> POST /v2/providers/employers/payrolladministrations/payrolltaxreturns/{payrolltaxreturnId}/undo
- "Create a withdrawIncomeRelationshipNumber?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrolltaxreturns/withdrawIncomeRelationshipNumber
- "List all address?" -> GET /locationservices/address
- "Search search?" -> GET /address/search
- "Search calculate?" -> GET /route/calculate
- "List all aowDate?" -> GET /aowDate
- "List all companyinformation?" -> GET /chamberofcommerce/{chamberOfCommerceNumber}/companyinformation
- "List all datanewbusinesstoken?" -> GET /v2/providers/employers/{employerId}/datanewbusinesstoken
- "List all token?" -> GET /datanewbusiness/token
- "List all functions?" -> GET /datanewbusiness/functions
- "List all availablehours?" -> GET /v2/providers/employers/{employerId}/employees/employments/calendar/availablehours
- "List all leave?" -> GET /v2/providers/employers/{employerId}/employees/employments/calendar/leave
- "List all leaverequests?" -> GET /v2/providers/employers/{employerId}/employees/employments/calendar/leaverequests
- "List all revokeleaverequests?" -> GET /v2/providers/employers/{employerId}/employees/employments/calendar/revokeleaverequests
- "List all absences?" -> GET /v2/providers/employers/{employerId}/employees/employments/calendar/absences
- "List all teamCalendar?" -> GET /v2/providers/employers/employees/employments/{employmentId}/teamCalendar
- "List all personalCalendar?" -> GET /v2/providers/employers/employees/employments/{employmentId}/personalCalendar
- "List all employmenttemplates?" -> GET /v2/providers/employers/{employerId}/employmenttemplates
- "Create a employmenttemplate?" -> POST /v2/providers/employers/{employerId}/employmenttemplates
- "Update a employmenttemplate?" -> PUT /v2/providers/employers/employmenttemplates/{employmenttemplateId}
- "Delete a employmenttemplate?" -> DELETE /v2/providers/employers/employmenttemplates/{employmenttemplateId}
- "List all declarations?" -> GET /v2/providers/employers/{employerId}/employees/employments/declarations
- "List all attachment?" -> GET /v2/providers/employers/employees/employments/declarations/{declarationId}/attachment
- "Create a attachment?" -> POST /v2/providers/employers/employees/employments/declarations/{declarationId}/attachment
- "List all withattachment?" -> GET /v2/providers/employers/{employerId}/employees/employments/declarations/withattachment
- "List all withattachment?" -> GET /v2/providers/employers/employees/employments/{employmentId}/declarations/withattachment
- "List all withattachment?" -> GET /qwoatermicroservice/providers/employers/employees/employments/declarations/withattachment
- "Create a initialise?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollperiods/initialise
- "Create a initiate?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollruns/initiate
- "List all initiationvalues?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollruns/{payrollPeriodId}/initiationvalues
- "Create a payrollrun?" -> POST /v2/providers/employers/payrolladministrations/payrollperiods/{payrollPeriodId}/payrollruns
- "Create a undo?" -> POST /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/undo
- "List all defaults?" -> GET /v2/providers/employers/employees/employments/{employmentId}/transitioncompensation/calculate/defaults
- "Create a calculate?" -> POST /v2/providers/employers/employees/employments/{employmentId}/transitioncompensation/calculate
- "List all documents?" -> GET /v2/providers/employers/employees/employments/{employmentId}/documents
- "Create a document?" -> POST /v2/providers/employers/employees/employments/{employmentId}/documents
- "Get document details?" -> GET /v2/providers/employers/employees/employments/{employmentId}/documents/{documentId}
- "Delete a document?" -> DELETE /v2/providers/employers/employees/employments/{employmentId}/documents/{documentId}
- "Update a document?" -> PUT /v2/providers/employers/employees/employments/{employmentId}/documents/{documentId}
- "List all audittrail?" -> GET /v2/providers/employers/employees/employments/{employmentId}/documents/{documentId}/audittrail
- "Get document details?" -> GET /v2/providers/employers/{employerId}/documents/{documentId}
- "Delete a document?" -> DELETE /v2/providers/employers/{employerId}/documents/{documentId}
- "Update a document?" -> PUT /v2/providers/employers/{employerId}/documents/{documentId}
- "List all documents?" -> GET /v2/providers/employers/{employerId}/documents
- "Create a document?" -> POST /v2/providers/employers/{employerId}/documents
- "List all audittrail?" -> GET /v2/providers/employers/{employerId}/documents/{documentId}/audittrail
- "Get document details?" -> GET /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents/{documentId}
- "Delete a document?" -> DELETE /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents/{documentId}
- "Update a document?" -> PUT /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents/{documentId}
- "List all documents?" -> GET /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents
- "Create a document?" -> POST /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents
- "List all audittrail?" -> GET /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents/{documentId}/audittrail
- "List all dossier"?" -> GET /v2/providers/employers/conceptemployees/{conceptEmployeeId}/dossier"
- "Get documenttemplate details?" -> GET /v2/providers/employers/{employerId}/documenttemplates/{documentId}
- "Delete a documenttemplate?" -> DELETE /v2/providers/employers/{employerId}/documenttemplates/{documentId}
- "Update a documenttemplate?" -> PUT /v2/providers/employers/{employerId}/documenttemplates/{documentId}
- "List all documenttemplates?" -> GET /v2/providers/employers/{employerId}/documenttemplates
- "Create a documenttemplate?" -> POST /v2/providers/employers/{employerId}/documenttemplates
- "Create a preview?" -> POST /v2/providers/employers/employees/employments/{employmentId}/documenttemplates/{documentId}/generatedocument/preview
- "Create a generatedocument?" -> POST /v2/providers/employers/employees/employments/{employmentId}/documenttemplates/{documentId}/generatedocument
- "Create a preview?" -> POST /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documenttemplates/{documentId}/generatedocument/preview
- "Create a generatedocument?" -> POST /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documenttemplates/{documentId}/generatedocument
- "Create a generatedocument?" -> POST /v2/providers/employers/{employerId}/documenttemplates/{documentId}/generatedocuments
- "List all report?" -> GET /v2/providers/employers/{employerId}/signature/report
- "Create a initiate?" -> POST /v2/providers/employers/employees/employments/{employmentId}/documents/{documentId}/signature/initiate
- "List all signature?" -> GET /v2/providers/employers/employees/employments/{employmentId}/documents/{documentId}/signature
- "List all report?" -> GET /v2/providers/employers/employees/employments/{employmentId}/documents/{documentId}/signature/report
- "Create a initiate?" -> POST /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents/{documentId}/signature/initiate
- "List all signature?" -> GET /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents/{documentId}/signature
- "List all report?" -> GET /v2/providers/employers/conceptemployees/{conceptEmployeeId}/documents/{documentId}/signature/report
- "List all authorizations?" -> GET /v2/providers/employers/{employerId}/documents/authorizations
- "Create a initiate?" -> POST /v2/providers/employers/{employerId}/documents/completedossier/initiate
- "List all report?" -> GET /v2/providers/employers/{employerId}/dossier/report
- "List all apgpensiondeclarations?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/apgpensiondeclarations
- "Get apgpensiondeclaration details?" -> GET /v2/providers/employers/payrolladministrations/apgpensiondeclarations/{apgPensionDeclarationId}
- "Partially update a apgpensiondeclaration?" -> PATCH /v2/providers/employers/payrolladministrations/apgpensiondeclarations/{apgPensionDeclarationId}
- "List all overview?" -> GET /v2/providers/employers/payrolladministrations/apgpensiondeclarations/{apgPensionDeclarationId}/overview
- "List all message?" -> GET /v2/providers/employers/payrolladministrations/apgpensiondeclarations/{apgPensionDeclarationId}/message
- "Create a initiate?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/apgpensiondeclarations/initiate
- "Create a initiateForPreviousYear?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/apgpensiondeclarations/initiateForPreviousYear
- "Create a undo?" -> POST /v2/providers/employers/payrolladministrations/apgpensiondeclarations/{apgPensionDeclarationId}/undo
- "List all upapensiondeclarations?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/upapensiondeclarations
- "Create a initiateforpreviousyear?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/externalparties/{externalPartyKey}/upapensiondeclarations/initiateforpreviousyear
- "Get upapensiondeclaration details?" -> GET /v2/providers/employers/payrolladministrations/upapensiondeclarations/{upaPensionDeclarationId}
- "Partially update a upapensiondeclaration?" -> PATCH /v2/providers/employers/payrolladministrations/upapensiondeclarations/{upaPensionDeclarationId}
- "Create a undo?" -> POST /v2/providers/employers/payrolladministrations/upapensiondeclarations/{upaPensionDeclarationId}/undo
- "List all message?" -> GET /v2/providers/employers/payrolladministrations/upapensiondeclarations/{upaPensionDeclarationId}/message
- "Create a initiate?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/externalparties/{externalPartyKey}/upapensiondeclarations/initiate
- "Create a pensiondeclaration?" -> POST /v2/providers/employers/payrolladministrations/payrollperiods/{payrollPeriodId}/pensiondeclarations
- "List all ExternalPartyIdentifications?" -> GET /v2/providers/{providerId}/ExternalPartyIdentifications
- "Create a ExternalPartyIdentification?" -> POST /v2/providers/{providerId}/ExternalPartyIdentifications
- "Get ExternalPartyIdentification details?" -> GET /v2/providers/ExternalPartyIdentifications/{externalPartyIdentificationId}
- "Update a ExternalPartyIdentification?" -> PUT /v2/providers/ExternalPartyIdentifications/{externalPartyIdentificationId}
- "Delete a ExternalPartyIdentification?" -> DELETE /v2/providers/ExternalPartyIdentifications/{externalPartyIdentificationId}
- "List all ExternalPartyIdentifications"?" -> GET /v2/providers/employers/payrollAdministrations/{payrollAdministrationId}/ExternalPartyIdentifications"
- "Create a ExternalPartyIdentifications"?" -> POST /v2/providers/employers/payrollAdministrations/{payrollAdministrationId}/ExternalPartyIdentifications"
- "Get ExternalPartyIdentification details?" -> GET /v2/providers/employers/payrollAdministrations/ExternalPartyIdentifications/{externalPartyIdentificationId}
- "Update a ExternalPartyIdentification?" -> PUT /v2/providers/employers/payrollAdministrations/ExternalPartyIdentifications/{externalPartyIdentificationId}
- "Delete a ExternalPartyIdentification?" -> DELETE /v2/providers/employers/payrollAdministrations/ExternalPartyIdentifications/{externalPartyIdentificationId}
- "List all pawwdeclarations?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pawwdeclarations
- "Create a initiate?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pawwdeclarations/initiate
- "Get pawwdeclaration details?" -> GET /v2/providers/employers/payrolladministrations/pawwdeclarations/{pawwDeclarationId}
- "Partially update a pawwdeclaration?" -> PATCH /v2/providers/employers/payrolladministrations/pawwdeclarations/{pawwDeclarationId}
- "List all message?" -> GET /v2/providers/employers/payrolladministrations/pawwdeclarations/{pawwDeclarationId}/message
- "Create a undo"?" -> POST /v2/providers/employers/payrolladministrations/pawwdeclarations/{pawwDeclarationId}/undo"
- "List all initiationvalues?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Stipp/initiationvalues
- "List all payrollRuns?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Stipp/payrollRuns
- "Create a Stipp?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Stipp
- "List all Stipp?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Stipp
- "List all initiationvalues?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Pggm/initiationvalues
- "List all payrollRuns?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Pggm/payrollRuns
- "Create a Pggm?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Pggm
- "List all Pggm?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/pensionWageStatement/Pggm
- "List all downloadrequests?" -> GET /v2/providers/employers/users/downloadrequests
- "Create a downloadrequest?" -> POST /v2/providers/employers/users/downloadrequests
- "Get downloadrequest details?" -> GET /v2/providers/employers/users/downloadrequests/{downloadRequestId}
- "Delete a downloadrequest?" -> DELETE /v2/providers/employers/users/downloadrequests/{downloadRequestId}
- "List all file?" -> GET /v2/providers/employers/users/downloadrequests/{downloadRequestId}/file
- "List all notes?" -> GET /v2/providers/employers/{employerId}/notes
- "Create a note?" -> POST /v2/providers/employers/{employerId}/notes
- "Get note details?" -> GET /v2/providers/employers/notes/{noteId}
- "Update a note?" -> PUT /v2/providers/employers/notes/{noteId}
- "Delete a note?" -> DELETE /v2/providers/employers/notes/{noteId}
- "List all notes?" -> GET /v2/providers/employers/employees/{employeeId}/notes
- "Create a note?" -> POST /v2/providers/employers/employees/{employeeId}/notes
- "Get note details?" -> GET /v2/providers/employers/employees/notes/{noteId}
- "Update a note?" -> PUT /v2/providers/employers/employees/notes/{noteId}
- "Delete a note?" -> DELETE /v2/providers/employers/employees/notes/{noteId}
- "List all notes?" -> GET /v2/providers/employers/{employerId}/employees/notes
- "List all notes?" -> GET /v2/providers/employers/conceptemployees/{conceptEmployeeId}/notes
- "Create a note?" -> POST /v2/providers/employers/conceptemployees/{conceptEmployeeId}/notes
- "Get note details?" -> GET /v2/providers/employers/conceptemployees/notes/{noteId}
- "Update a note?" -> PUT /v2/providers/employers/conceptemployees/notes/{noteId}
- "Delete a note?" -> DELETE /v2/providers/employers/conceptemployees/notes/{noteId}
- "List all notes?" -> GET /v2/providers/employers/employees/employments/{employmentId}/notes
- "Create a note?" -> POST /v2/providers/employers/employees/employments/{employmentId}/notes
- "Get note details?" -> GET /v2/providers/employers/employees/employments/notes/{noteId}
- "Update a note?" -> PUT /v2/providers/employers/employees/employments/notes/{noteId}
- "Delete a note?" -> DELETE /v2/providers/employers/employees/employments/notes/{noteId}
- "List all notes?" -> GET /v2/providers/employers/{employerId}/employees/employments/notes
- "List all notes?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/notes
- "Create a note?" -> POST /v2/providers/employers/payrolladministrations/payrollruns/{payrollrunId}/notes
- "Get note details?" -> GET /v2/providers/employers/payrolladministrations/payrollruns/notes/{noteId}
- "Update a note?" -> PUT /v2/providers/employers/payrolladministrations/payrollruns/notes/{noteId}
- "Delete a note?" -> DELETE /v2/providers/employers/payrolladministrations/payrollruns/notes/{noteId}
- "List all notes?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/payrollruns/notes
- "List all lastmodifiedversionnumbers?" -> GET /v2/providers/employers/lastmodifiedversionnumbers
- "List all lastmodifiedversionnumbers?" -> GET /v2/providers/employers/{employerId}/employees/employments/lastmodifiedversionnumbers
- "List all emailtemplates?" -> GET /v2/providers/{providerId}/emailtemplates
- "Get emailtemplate details?" -> GET /v2/providers/{providerId}/emailtemplates/{emailTemplateId}
- "Update a emailtemplate?" -> PUT /v2/providers/{providerId}/emailtemplates/{emailTemplateId}
- "Delete a emailtemplate?" -> DELETE /v2/providers/{providerId}/emailtemplates/{emailTemplateId}
- "List all emailtemplates?" -> GET /v2/providers/employers/{employerId}/emailtemplates
- "Get emailtemplate details?" -> GET /v2/providers/employers/{employerId}/emailtemplates/{emailTemplateId}
- "Update a emailtemplate?" -> PUT /v2/providers/employers/{employerId}/emailtemplates/{emailTemplateId}
- "Delete a emailtemplate?" -> DELETE /v2/providers/employers/{employerId}/emailtemplates/{emailTemplateId}
- "List all eventnotificationconfigurations?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/eventnotificationconfigurations
- "Get eventnotificationconfiguration details?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/eventnotificationconfigurations/{eventTypeId}
- "Update a eventnotificationconfiguration?" -> PUT /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/eventnotificationconfigurations/{eventTypeId}
- "Delete a eventnotificationconfiguration?" -> DELETE /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/eventnotificationconfigurations/{eventTypeId}
- "List all eventnotificationconfigurations?" -> GET /v2/providers/{providerId}/eventnotificationconfigurations
- "Get eventnotificationconfiguration details?" -> GET /v2/providers/{providerId}/eventnotificationconfigurations/{eventTypeId}
- "Update a eventnotificationconfiguration?" -> PUT /v2/providers/{providerId}/eventnotificationconfigurations/{eventTypeId}
- "Delete a eventnotificationconfiguration?" -> DELETE /v2/providers/{providerId}/eventnotificationconfigurations/{eventTypeId}
- "List all authorizations?" -> GET /applications/{applicationId}/authorizations
- "List all logo?" -> GET /applications/{applicationId}/logo
- "List all applications?" -> GET /v2/providers/employers/{employerId}/applications
- "List all users?" -> GET /v2/providers/employers/{employerId}/applications/{applicationId}/users
- "Create a registerInterest"?" -> POST /v2/providers/employers/{employerId}/applications/{applicationId}/registerInterest"
- "List all employerData?" -> GET /v2/providers/employers/{employerId}/auditTrail/employerData
- "List all employeeData?" -> GET /v2/providers/employers/{employerId}/auditTrail/employeeData
- "List all PayrollPeriodData?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/auditTrail/PayrollPeriodData
- "List all applicationsets?" -> GET /applicationset/providers/employers/{employerId}/applicationsets
- "Create a applicationset?" -> POST /applicationset/providers/employers/{employerId}/applicationsets
- "Update a applicationset?" -> PUT /applicationset/providers/employers/applicationsets/{applicationSetId}
- "Delete a applicationset?" -> DELETE /applicationset/providers/employers/applicationsets/{applicationSetId}
- "List all applicationsets?" -> GET /applicationset/providers/{providerId}/applicationsets
- "Create a applicationset?" -> POST /applicationset/providers/{providerId}/applicationsets
- "Update a applicationset?" -> PUT /applicationset/providers/applicationsets/{applicationSetId}
- "Delete a applicationset?" -> DELETE /applicationset/providers/applicationsets/{applicationSetId}
- "List all applicationsets?" -> GET /applicationset/users/{userId}/applicationsets
- "Create a applicationset?" -> POST /applicationset/users/{userId}/applicationsets
- "Update a applicationset?" -> PUT /applicationset/users/applicationsets/{applicationSetId}
- "Delete a applicationset?" -> DELETE /applicationset/users/applicationsets/{applicationSetId}
- "List all general?" -> GET /applicationset/applicationsets/general
- "List all payrollSimulatorData?" -> GET /v2/providers/employers/employees/employments/{employmentId}/payrollSimulatorData
- "List all emailidentities?" -> GET /v2/providers/{providerId}/emailidentities
- "Create a emailidentity?" -> POST /v2/providers/{providerId}/emailidentities
- "Delete a emailidentity?" -> DELETE /v2/providers/emailidentities/{emailIdentityId}
- "Create a sendtestemail?" -> POST /v2/providers/emailidentities/{emailIdentityId}/sendtestemail
- "Create a verify?" -> POST /v2/providers/{providerId}/emailidentities/verify
- "List all emailidentities?" -> GET /v2/providers/employers/{employerId}/emailidentities
- "Create a emailidentity?" -> POST /v2/providers/employers/{employerId}/emailidentities
- "Delete a emailidentity?" -> DELETE /v2/providers/employers/emailidentities/{emailIdentityId}
- "Create a sendtestemail?" -> POST /v2/providers/employers/emailidentities/{emailIdentityId}/sendtestemail
- "Create a verify?" -> POST /v2/providers/employers/{employerId}/emailidentities/verify
- "Partially update a import?" -> PATCH /v2/providers/employers/conceptemployees/import/{payrollAdministrationId}
- "Create a employee?" -> POST /v2/providers/employers/payrollAdministrations/{payrollAdministrationId}/import/employees
- "List all WageProposals?" -> GET /v2/providers/employers/{employerId}/employees/employments/WageProposals
- "Create a initialize?" -> POST /v2/providers/employers/{employerId}/proforma/initialize
- "List all proforma?" -> GET /v2/providers/employers/{employerId}/proforma
- "List all workRelatedCostsSchemeFinancials?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/workRelatedCostsSchemeFinancials
- "Create a workRelatedCostsSchemeFinancial?" -> POST /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/workRelatedCostsSchemeFinancials
- "Get workRelatedCostsSchemeFinancial details?" -> GET /v2/providers/employers/payrolladministrations/workRelatedCostsSchemeFinancials/{workRelatedCostsSchemeFinancialId}
- "Update a workRelatedCostsSchemeFinancial?" -> PUT /v2/providers/employers/payrolladministrations/workRelatedCostsSchemeFinancials/{workRelatedCostsSchemeFinancialId}
- "Delete a workRelatedCostsSchemeFinancial?" -> DELETE /v2/providers/employers/payrolladministrations/workRelatedCostsSchemeFinancials/{workRelatedCostsSchemeFinancialId}
- "List all workRelatedCostsSchemeMatrix?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/workRelatedCostsSchemeMatrix
- "List all workRelatedCostsSchemeReport?" -> GET /v2/providers/employers/payrolladministrations/{payrollAdministrationId}/workRelatedCostsSchemeReport
- "List all modules?" -> GET /provider/providers/{providerId}/employers/modules
- "List all YearEndStatements?" -> GET /provider/providers/{providerId}/payrollAdministrations/YearEndStatements
- "List all Payslips?" -> GET /provider/providers/{providerId}/payrollAdministrations/Payslips
- "List all employmentTurnover?" -> GET /provider/providers/{providerId}/payrollAdministrations/employmentTurnover
- "List all report?" -> GET /payrolltaxreturn/providers/employers/payrolladministrations/payrolltaxreturns/{payrollTaxReturnId}/report
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
