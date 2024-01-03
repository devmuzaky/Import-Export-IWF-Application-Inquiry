# Import\Export | IWF - Application Inquiry (360 view)

[//]: # (Here is the comments for the Two tables in the page) 
## According to customer
- as per call with the PO, there are a difference between the "تصنيف النشاط" -- &  -- "تصنيف mis-activity".
- so what shall we do with the "تصنيف mis-activity" ?? in the high-risk table.

## According to Maker
- Firstly the Fields in the CustomerDetails arranged in a different order than the order in high-risk table.
- Secondly, there is a new field in the CustomerDetails called "نوع النشاط" which is not in the high-risk table.


###  بيانات الشركة Section - وصف النشاط وفقاً لافادة العميل Table
- I want to review all conditions for the fields and if any condition is difference with the high-risk table.
  ![image.png](image.png)


[//]: # (create a red line under this )



`-__-__-__-__-__________________Errors_____________________-__-__-__-__-`

### Import & Export Errors - Acceptance Criteria | Display return to Customer
- Firstly, all those codes should be written in  <code> application-rejection-reasons</code>
- Secondly, the error color should be red not rose I think in the new user story.
- Lastly, for the <strong>error codes</strong> <code>EXM12002</code>, <code>EXM12008</code> and <code>EXM12012</code>, the error message is containing two messages.
How to display the two messages in the return to customer?
![image_1.png](image_1.png)

How to handle displaying two messages in the return to customer?
the solution from my perspective is to create a  method to extract the activity type, so we can customize the error message for "EXM12008" based on the activity type.
<code>
```getErrorMessage(reason: any): string {
  if (reason['code'] === 'EXM12008') {
    const activityType = getActivityTypeFromTitle(reason['title']);
    if (activityType === 'نشاط الاستيراد') {
      return 'من واقع السجل التجاري تبين أن نوع نشاط الاستيراد هو ($Maker’s Selection) ولا يتوافق وصف نشاط الاستيراد بالسجل مع افادتكم، يرجى ادخال تفاصيل اضافية لنشاط الاستيراد';
    } else if (activityType === 'نشاط التصدير') {
      return 'من واقع السجل التجاري تبين أن نوع نشاط التصدير هو ($Maker’s Selection) ولا يتوافق وصف نشاط التصدير بالسجل مع افادتكم، يرجى ادخال تفاصيل اضافية لنشاط التصدير';
    }
  }
  return ''; // Default message or handle other error codes
}
```
</code>


### Import & Export Errors - Acceptance Criteria | Risk Type
- it should be reusable component? or it is only used in this page?
- wanna review the conditions for the risk type.
