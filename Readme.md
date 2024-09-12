# **Reebelo Product & Order Management System**

### **Overview**

This project is a full-stack web application that simulates a product and order management system. It includes the ability to create, update, and view products and orders while providing scalability and a clear path to millions of users and products.

### **Technologies Used**

- **Frontend**: React with TypeScript
- **Backend**: Node.js with Express and MongoDB (Mongoose)
- **State Management**: Redux Toolkit
- **API Communication**: Axios
- **Styling**: React-Bootstrap
- **State Management**: Redux Toolkit
- **Toast Notifications**: react-toastify
- **AWS Services** (Architecture based, not fully deployed):
  - **API Gateway**: For routing API requests.
  - **AWS Lambda**: Serverless function to handle the backend logic.
  - **DynamoDB**: To store product and order data in a scalable way.
  - **S3**: To serve static assets.
  - **CloudFront**: To distribute the frontend with low latency and high performance.

---

## **How to Run Locally**

### **Frontend Setup**

1. **Clone the repository**

   ```bash
   git clone <repository-url>
   cd frontend
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Set up environment variables**
   Create a `.env` file in the `frontend/` folder and add your API base URL.

   ```bash
   REACT_APP_API_BASE_URL=http://localhost:5000
   ```

4. **Run the development server**
   ```bash
   npm start
   ```

### **Backend Setup**

1. **Go to the backend directory**

   ```bash
   cd backend
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Set up environment variables**
   Create a `.env` file in the `backend/` folder with the following content:

   ```bash
   MONGODB_URI=<your-mongodb-uri>
   ```

4. **Start the server**

   ```bash
   npm run start
   ```

5. **Backend endpoints**
   - `POST /api/products` – Create a product.
   - `PUT /api/products/:id` – Update a product.
   - `POST /api/orders` – Create an order.
   - `PATCH /api/orders/:id/status` – Update order status.
   - `PUT /api/orders/:id/shipping` – Update order shipping.

---

## **AWS Architecture Design**

Here’s the architecture for deploying this application on AWS for scalability and performance:

### **Architecture Diagram**

```
User -> CloudFront -> S3 -> API Gateway -> Lambda -> DynamoDB
```

### **AWS Services and Explanation**

1. **Amazon S3**:

   - **Why**: Used to serve the static assets (React frontend). S3 offers durability and scalability for hosting frontend code.
   - **Opportunity**: S3 ensures the site is available globally with low latency using CloudFront.

2. **AWS CloudFront**:

   - **Why**: A Content Delivery Network (CDN) service that speeds up the distribution of static content to users.
   - **Opportunity**: Helps serve assets quickly to a global audience.

3. **Amazon API Gateway**:

   - **Why**: API Gateway allows for routing API calls securely and efficiently.
   - **Opportunity**: It can scale automatically based on the number of API requests, ensuring high availability and performance.

4. **AWS Lambda**:

   - **Why**: Lambda allows for running backend functions in a serverless way, which is both cost-effective and scalable.
   - **Opportunity**: The serverless model helps scale backend services easily, especially during traffic spikes.

5. **Amazon DynamoDB**:
   - **Why**: A fully managed NoSQL database that is highly scalable and fast, making it perfect for storing products and orders.
   - **Opportunity**: DynamoDB can scale to handle millions of requests per second, ensuring smooth performance even under heavy loads.

---

## **Scalability Considerations**

- **Serverless Architecture**: Using Lambda and API Gateway ensures that we can scale without worrying about server management. AWS automatically provisions the infrastructure based on demand.
- **DynamoDB**: DynamoDB is capable of handling large-scale read and write operations, which is essential for millions of products and orders.
- **Stateless Frontend**: The React app is completely stateless, allowing the use of CDN (CloudFront) to distribute it globally with minimum delay.

---

## **Opportunities and Limitations**

### **Opportunities**

- **Serverless Computing**: AWS Lambda reduces infrastructure management, allowing for faster scaling as more users access the application.
- **Low Latency**: CloudFront ensures static files are distributed globally, enhancing load times for users.
- **Cost Efficiency**: By using AWS services like Lambda, DynamoDB, and S3, costs are kept in check by only paying for the resources used.

### **Known Limitations**

- **Cold Starts**: AWS Lambda may experience cold starts when it's not in use, resulting in a slight delay for some requests.
- **Limited Real-Time Data**: DynamoDB is eventually consistent, which may cause slight delays in real-time updates.
