# KinderCare Notes
* AWS Tools
  * Amazon Rekognition - image processing
* Use Java for tools
  * Birt
    * Statements
    * Weekly attendance register
    * Printable reports
## Admin UI
* Home
  * Welcome
  * Updates
  * Reminders
* Children
  * Search for children
  * List all children
    * Sort by class
    * Sort by first
    * Sort by last
  * Accounting
    * Children by account outstanding
* Accounting
  * Search for child
    * Payments (receipts)
    * Adjustments
    * Line Items (add new items to child account)
  * Registration
    * Add new student
## KinderCare Notes
* Create an admin interface for students.
  * Registration
    * Check if student exists using the id attribute
    * Add new child
      * Child information
      * Parent/guardian information
      * Parent employment information
      * Authorized persons
      * Payment information
  * Payment
    * Find student/account
    * Receipt Id
    * Amount
    * Type
    * Notes
  * Line Items
    * Add individual line items
    * Notes
  * Batch items
    * Line item
    * Select individual students
    * Update the students
  * Month-end processing
    * Cut-off date
    * Process students
* Models
  * Account
    * Students
    * Parents
    * Authorized Persons
  * Accounting
    * Account
    * Receipts
    * Line Items
    * Adjustments
  * Class
    * Students
