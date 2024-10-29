# Salesforce Triggers Documentation

## Trigger 1: Automatically Create a Follow-Up Case After One Month

**Trigger Name:** `StudentTrigger`

**Trigger Event:** `after update`

**Description:**
This trigger automatically creates a follow-up case for students who have been enrolled for a month. The case is created to ensure continuous support and engagement with students after one month in the program.

**Trigger Logic:**
1. Check if the student's `Enrollment_Date__c` was one month ago and if `Last_Follow_Up__c` is `null`.
2. If both conditions are met, create a high-priority case with:
   - Subject: `One Month Follow-up`
   - Description: A message to ensure ongoing support after one month of enrollment.
3. Add cases to a list and insert them in bulk to minimize DML operations.
4. Implement error handling to alert if case creation fails.
## Trigger 2: Send Email Reminder for Upcoming Appointments 24 Hours in Advance

**Trigger Name:** `AppointmentReminderTrigger`

**Trigger Event:** `before update`

**Purpose:**  
This trigger is designed to send automated reminder emails to both students and consultants 24 hours before a scheduled appointment. It helps ensure that both parties are reminded of their upcoming appointments, reducing the likelihood of missed sessions.

### Trigger Workflow:
1. **Calculate Time Difference**: The trigger calculates the time difference between the current date and time and the scheduled appointment time (`Appointment_Date__c` and `Appointment_Time__c` fields).
2. **Check Reminder Criteria**: 
   - If the appointment is exactly 24 hours away.
   - If the `Reminder_Sent__c` field is set to `false` (to avoid sending duplicate reminders).
3. **Send Reminder Emails**: 
   - Retrieve email addresses for both the student and consultant.
   - Create a reminder email for each party with appointment details.
4. **Update Appointment Record**: Set `Reminder_Sent__c` to `true` after the email is sent to avoid duplicate reminders in future trigger executions.
