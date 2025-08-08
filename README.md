

# HandsMen Threads: Elevating the Art of Sophistication in Men's Fashion

## ABSTRACT

This project describes how we built a customized Salesforce CRM solution for HandsMen Threads, which is a premium men's fashion and tailoring brand. Our goal was to make business operations smoother, improve customer engagement, and keep data accurate across all departments.

We designed a strong data model with five important custom objects: Customer, Order, Product, Inventory, and Marketing Campaign. We automated business processes by using Record-Triggered Flows, Scheduled Flows, Email Alerts, and Apex. These help with order confirmations, loyalty status updates, and stock alerts that work automatically.

We created validation rules to keep data clean and reliable. We also set up a role-based security model for the Sales, Inventory, and Marketing teams. The solution includes a scheduled batch job that uses Apex to update low stock quantities automatically.

This complete CRM implementation makes customer experience better through personalized communication. It ensures operations run smoothly with automation and creates a scalable foundation for future business growth using the Salesforce Platform.

## OBJECTIVE

The main goal of this project is to create and implement a customized Salesforce CRM solution for HandsMen Threads. This will help streamline core business operations, maintain data accuracy, and improve customer satisfaction.

We built a centralized system to manage customers, orders, products, inventory, and marketing campaigns. The project aims to:

- Make key processes automatic, such as order confirmations, loyalty status updates, and stock alerts
- Make sure data entry is accurate and consistent by using validation rules
- Provide real-time visibility of inventory and customer interactions
- Make internal team coordination better through role-based access control
- Give personalized customer experiences through targeted communication and loyalty programs


## TECHNOLOGY DESCRIPTION

**Salesforce:**
Salesforce is a cloud-based Customer Relationship Management (CRM) platform. It helps businesses manage customer data, automate processes, and improve service, marketing, and sales operations. It provides easy-to-use tools and programming capabilities (like Apex and Flows) to build custom business solutions.

**Custom Objects:**
Objects in Salesforce work like tables in a database. We create Custom Objects to store specific data.

Examples:

- Customer - Stores customer information
- Product - Stores product details
- Order - Stores order information

**Tabs:**
Tabs help display object data in the Salesforce user interface.

Example: A tab for Product allows users to easily view and manage products.

**Custom App:**
An App in Salesforce is a group of tabs put together for a specific business purpose.

**Profiles:**
Profiles decide what a user can see, do, and edit in Salesforce. They control object permissions, field access, and more.

**Roles:**
Roles control data visibility in Salesforce's role hierarchy. They are used for sharing settings and reporting.

**Permission Sets:**
Permission Sets give additional permissions to users without changing their profile.

**Validation Rules:**
Validation Rules make sure the data entered meets business requirements.

Examples:

- Email must contain @gmail.com
- Stock cannot be negative

**Email Templates:**
These are pre-made formats for sending emails to customers or users.

Example: "Order Confirmation" template

**Email Alerts:**
Email Alerts are actions in Flows or Workflow Rules that send emails using pre-made templates.

Example: When a loyalty level changes, the system sends an email to the customer.

**Flows:**
Flows automate business logic without writing code. They can create, update, or send notifications.

Example: Flow triggers email alerts when there is a new order

**Apex:**
Apex is Salesforce's object-oriented programming language. It lets developers write custom logic.

Example Triggers:

- Update Total Amount in orders
- Reduce inventory stock


## DETAILED EXECUTION OF PROJECT PHASES

### 1. Developer Org Setup

We created a Salesforce Developer Org using https://developer.salesforce.com/signup.
We verified the account, set the password, and got access to the Salesforce Setup page.

### 2. Custom Object Creation

We created five custom objects to store important business data:

- **HandsMen Customer** - Stores customer information like email, phone, loyalty status
- **HandsMen Product** - Stores product catalog details like SKU, price, and stock
- **HandsMen Order** - Stores orders placed by customers, including quantity and status
- **Inventory** - Tracks stock quantity and warehouse location
- **Marketing Campaign** - Stores promotional campaigns and scheduling

Steps we followed:

- Went to Setup → Object Manager → Create Custom Object
- Added label, name, and enabled reports/search
- Saved and created Tabs for each object


### 3. Creating the Lightning App

We created a custom Lightning App named HandsMen Threads.
We included tabs: HandsMen Customer, Order, Product, Inventory, Campaign, Reports, etc.
We assigned it to the System Administrator profile.

### 4. Validation Rules

To make sure data entry is accurate and follows business logic, we applied these validation rules:

- **Order Object**: Stops saving if Total Amount is 0. Error message: "Please Enter Correct Amount"
- **Customer Object**: Checks that email contains @gmail.com. Error message: "Please fill Correct Gmail"


### 5. User Role \& Profile Setup

We copied the Standard User profile to create a new profile named Platform 1. We added access to necessary custom objects.
We created roles for different departments:

- Sales Manager
- Inventory Manager
- Marketing Team


### 6. User Creation

We created users in Salesforce and gave them appropriate roles and profiles based on their responsibilities:

- **Niklaus Mikaelson** - Given the Sales role
- **Kol Mikaelson** - Given the Inventory role

These role-based assignments help enforce proper data access and process control within the system.

### 7. Email Template \& Alerts

We created three email templates:

- **Order Confirmation** - Sent when order status is Confirmed
- **Low Stock Alert** - Sent when Inventory is less than 5 units
- **Loyalty Program Email** - Sent when loyalty status changes

We created corresponding Email Alerts using these templates and linked them to automation flows.

### 8. Flow Implementations

**a. Order Confirmation Flow**

- Triggers when an order is updated to Confirmed
- Sends an Order Confirmation email to the related customer

**b. Stock Alert Flow**

- Triggers when Inventory stock drops below 5
- Sends Low Stock email to Inventory Manager

**c. Scheduled Flow: Loyalty Update**

- Runs daily at midnight
- Goes through customers and updates their Loyalty Status based on total purchases


### 9. Apex Triggers

- **Order Total Trigger**: Automatically calculates Total Amount based on quantity and unit price
- **Stock Deduction Trigger**: Reduces stock when an order is placed
- **Loyalty Status Trigger**: Updates Loyalty Status based on total purchases

## PROJECT EXPLANATION WITH REAL-WORLD EXAMPLE

Let's see how this works with a real customer interaction.

### 1. Customer Registration

A customer, **Elijah Mikaelson**, visits the store or website.
In Salesforce: We create a record in the Customer object with his name, phone, email, etc.
Validation Rule: Makes sure the email is valid (must contain @gmail.com).

### 2. Product Setup

The admin adds products like Shirts, Jeans, etc., into the Product object.
Each product has a price and other details.
We also create Inventory records to manage stock for these products.

### 3. Order Placement

Elijah decides to buy 2 shirts (each ₹500). An order gets placed.
In Salesforce: We create a new Order record.
Apex Trigger: Automatically calculates Total Amount = ₹500 × 2 = ₹1000.

### 4. Inventory Update

As soon as the order is placed:
Apex Trigger on Inventory: Reduces shirt stock by 2.
Validation Rule: Makes sure stock never goes below 0.

### 5. Loyalty Program

Elijah now has a total purchase of ₹1000.
A trigger on Customer checks his total purchases.
Based on the value:

- Less than ₹500 = Bronze
- ₹500-₹1000 = Silver
- More than ₹1000 = Gold

So, Elijah becomes a Silver member.

### 6. Email Notifications

When a new order is placed or loyalty status is updated:
Flow + Email Alert gets triggered.
Elijah receives an email:
"Thanks for your purchase! Your loyalty status is now Silver."

### 7. Users and Roles

Salesforce users like store staff are created:

- **Niklaus Mikaelson** - Sales Role (Platform 1 Profile)
- **Kol Mikaelson** - Inventory Role (Platform 1 Profile)


## CONCLUSION

The HandsMen Threads CRM system built on Salesforce successfully makes key business processes smoother. These include customer management, product cataloging, order processing, inventory tracking, and loyalty program automation. By using Salesforce tools like Custom Objects, Flows, Validation Rules, Email Alerts, and Apex, the system makes sure data entry is accurate, updates happen in real-time, and customer experience is enhanced. Through automation and well-organized user roles, the platform reduces manual errors, makes operations faster, and provides better insights into sales and stock.

## Future Scope:

### 1. Customer Portal Integration

Build a Customer Community Portal where customers can log in, view orders, and track loyalty status.

### 2. Mobile App using Salesforce Mobile SDK

Allow store staff to manage inventory and orders on the go using a mobile interface.

### 3. Reports \& Dashboard

Create detailed sales and inventory dashboards for management to monitor trends and performance in real-time.

### 4. AI-Powered Recommendations (Einstein)

Use Salesforce Einstein to provide personalized product suggestions based on past purchases.

### 5. WhatsApp/SMS Integration

Notify customers via WhatsApp or SMS about order confirmations and loyalty updates.

