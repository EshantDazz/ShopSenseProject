# ShopSense: Smart Shopping Assistant 🛍️

A powerful browser extension and chatbot system that tracks your e-commerce browsing activities and provides intelligent shopping recommendations using LLM technology.

## 🌟 Features

- **E-commerce Activity Tracking**: Browser extension that monitors and stores your shopping activities across various websites
- **Intelligent Product Database**: Automatically scrapes and stores detailed product information including prices, descriptions, and historical data
- **Credit Card Recommendations**: Smart system to suggest the best credit cards for specific purchases
- **Natural Language Interface**: Chat with the assistant to get personalized shopping insights
- **User Authentication**: Secure login system to protect your shopping data

## 🏗️ System Architecture

### Database Schema

```sql
CREATE TABLE Users (
   user_id INT PRIMARY KEY,
   email VARCHAR(255),
   name VARCHAR(100),
   created_at TIMESTAMP
);

CREATE TABLE Products (
   product_id INT PRIMARY KEY,
   product_link TEXT,
   website_company_name VARCHAR(100),
   prodct_name VARCHAR(255),
   description TEXT,
   category VARCHAR(100),
   current_price DECIMAL(10,2),
   original_price DECIMAL(10,2),
   discount_percentage DECIMAL(5,2),
   brand VARCHAR(100),
   availability_status BOOLEAN,
   last_updated TIMESTAMP
);

CREATE TABLE UserProductInteractions (
   interaction_id INT PRIMARY KEY,
   user_id INT,
   product_id INT,
   interaction_type VARCHAR(100),
   interaction_date TIMESTAMP,
   FOREIGN KEY (user_id) REFERENCES Users(user_id),
   FOREIGN KEY (product_id) REFERENCES Products(product_id)
);

CREATE TABLE CreditCards (
   card_id INT PRIMARY KEY,
   card_name VARCHAR(100),
   bank_name VARCHAR(100),
   reward_rate DECIMAL(4,2),
   cashback_categories JSON,
   annual_fee DECIMAL(10,2),
   special_offers TEXT
);

CREATE TABLE ProductCardBenefits (
   benefit_id INT PRIMARY KEY,
   product_id INT,
   card_id INT,
   benefit_type VARCHAR(50),
   benefit_value DECIMAL(5,2),
   valid_until DATE,
   FOREIGN KEY (product_id) REFERENCES Products(product_id),
   FOREIGN KEY (card_id) REFERENCES CreditCards(card_id)
);
```

## 🚀 Technology Stack

- **Backend**: FastAPI
- **Database**: PostgreSQL
- **LLM Integration**: LangChain with Groq (llama-3.3-70b-versatile model)
- **Frontend**: Jinja2 Templates
- **Authentication**: Session-based authentication

## 💬 Chatbot Capabilities

The intelligent shopping assistant can answer questions like:
- "What products did I view yesterday?"
- "Which credit card is best for purchasing Product X?"
- "Show me the items with highest discounts in the Men's Fashion category"
- "What are the current offers on electronics?"

## 🔧 Setup and Installation

1. Clone the repository
```bash
git clone https://github.com/yourusername/shopsense.git
cd shopsense
```

2. Install dependencies
```bash
pip install -r requirements.txt
```

3. Set up environment variables
```bash
cp .env.example .env
# Edit .env with your configuration
```

4. Initialize the database
```bash
# Run the SQL scripts to create tables
```

5. Run the application
```bash
uvicorn main:app --reload
```

## 🔐 Authentication

The system uses a simple session-based authentication system. Users can:
- Login with email and password
- Access their personalized shopping data
- Maintain secure sessions

## 📚 API Routes

### Chat Endpoints
- `GET /chat`: Renders the chat interface
- `POST /api/chat`: Processes chat messages and returns AI responses

### Authentication Endpoints
- `GET /login`: Renders login page
- `POST /login`: Processes login requests
- `GET /logout`: Handles user logout

## 🌐 Browser Extension

The browser extension component:
- Tracks product views across e-commerce sites
- Monitors wishlist and cart additions
- Securely sends data to the backend
- Maintains user privacy

## 🤖 LLM Integration

The system uses LangChain with Groq's llama-3.3-70b-versatile model for:
- Natural language understanding
- Query generation
- Response formatting
- Contextual recommendations

## 📊 Data Processing

- Web scraping for product details
- Real-time price tracking
- Credit card benefit analysis
- User interaction history management

## 🛣️ Future Roadmap

- [ ] Price history visualization
- [ ] Deal alerts system
- [ ] Mobile app integration
- [ ] Multi-language support
- [ ] Advanced analytics dashboard

## 👥 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.


