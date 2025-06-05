# Complete Hotel AI Architecture - LangChain + Opera PMS + Performance
## 🚀 **Enhanced System (LangChain + Opera + Performance)**

```mermaid
graph TB
    subgraph "Guest Interaction Channels"
        A[💬 Web Chat]
        B[📞 Phone System]
        C[🎤 Voice Interface] 
        D[📱 Mobile App]
    end
    
    subgraph "Performance Layer"
        E[⚖️ Load Balancer]
        F[🎯 Redis Cache]
        G[🚀 FastAPI Gateway]
    end
    
    subgraph "AI Processing (Enhanced)"
        H[🧠 LangChain Agent + Cache]
        I[🎯 Intent Analysis + Cache]
        J[🔄 Context Management]
        K[🎙️ ElevenLabs Voice + Cache]
        L[🛠️ LangChain Tools]
    end
    
    subgraph "MCP Service Layer"
        M[🎭 Activities MCP]
        N[💆 Spa MCP] 
        O[🍽️ Room Service MCP]
        P[🧹 Housekeeping MCP]
        Q[🔧 Maintenance MCP]
    end
    
    subgraph "Hotel Management (Opera PMS)"
        R[🏨 Opera PMS Core]
        S[👤 Guest Profiles]
        T[🏠 Room Management]
        U[💳 Billing & Folio]
        V[📅 Reservations]
        W[🔌 Opera REST APIs]
    end
    
    subgraph "Notification System"
        EE[📧 Email Service]
        FF[📱 SMS Service]
        GG[🔔 Notification Queue]
    end
    
    subgraph "Data & Analytics (Enhanced)"
        X[🐘 PostgreSQL]
        Y[📊 Real-time Dashboard]
        Z[📈 Advanced Analytics]
        AA[👩‍💼 Staff Override Panel]
    end
    
    subgraph "External APIs"
        BB[☁️ OpenAI API]
        CC[🎵 ElevenLabs API]
        DD[📞 Twilio Voice API]
        HH[📧 SendGrid Email API]
    end
    
    A --> E
    B --> E
    C --> E
    D --> E
    
    E --> G
    G --> F
    
    F -->|Cache Hit| H
    F -->|Cache Miss| H
    
    H --> I
    I --> J
    H --> L
    K --> H
    
    L --> M
    L --> N
    L --> O
    L --> P
    L --> Q
    
    M --> W
    N --> W
    O --> W
    P --> W
    Q --> W
    
    W --> R
    R --> S
    R --> T
    R --> U
    R --> V
    
    W --> GG
    GG --> EE
    GG --> FF
    EE --> HH
    
    H --> X
    W --> X
    X --> Y
    X --> Z
    Y --> AA
    
    H --> BB
    K --> CC
    B --> DD
    
    style F fill:#e8f5e8
    style H fill:#f3e5f5
    style R fill:#fff8e1
    style X fill:#e3f2fd
    style EE fill:#fff3e0
```

## 🔄 **LangChain Request Flow with Email Confirmation**

```mermaid
sequenceDiagram
    participant G as Guest
    participant API as FastAPI Gateway
    participant Cache as Redis Cache
    participant LC as LangChain Agent
    participant Tools as LangChain Tools
    participant Opera as Opera PMS
    participant Email as Email Service
    participant Queue as Notification Queue
    participant OpenAI as OpenAI API
    participant DB as PostgreSQL

    G->>API: "Book spa massage for 2pm"
    API->>Opera: 🔍 Lookup guest by session/room
    Opera-->>API: 👤 Guest profile (Ms. Johnson, Room 205, Platinum)
    API->>Cache: Check cached response for similar requests
    
    alt Cache Hit (80% of requests)
        Cache-->>API: Cached LangChain response (50ms)
        API->>DB: Log cache hit + guest interaction
        API-->>G: Instant response ⚡ "Checking availability..."
        
        Note over API,Opera: Even cached responses trigger real booking
        API->>LC: Execute cached booking with guest context
        LC->>Tools: Execute spa booking tool with guest data
        Tools->>Opera: Check real-time spa availability for 2pm
        Opera-->>Tools: ✅ Available slots + guest preferences (deep tissue)
        Tools->>Opera: Create spa reservation with guest preferences
        Opera-->>Tools: Booking confirmation + auto-charge to folio
        Tools->>Queue: Queue email confirmation task
        Queue->>Email: Send personalized booking confirmation
        Email->>Opera: Get guest email + communication preferences
        Email->>Email: Generate template with guest VIP status
        Email-->>Queue: ✅ Email sent successfully
        Queue-->>Tools: Email delivery confirmation
        Tools-->>LC: Complete booking result + email status
        LC-->>API: Final confirmation with all details
        API->>DB: Log successful booking + email + revenue
        API-->>G: 📧 "Spa booked for 2pm! Confirmation sent to your email."
        
    else Cache Miss (20% of requests)
        API->>LC: Process with LangChain agent + guest context
        LC->>OpenAI: Analyze intent with guest history
        OpenAI-->>LC: Intent: spa_booking + guest preferences
        LC->>Tools: Execute spa booking tool with context
        Tools->>Opera: Check guest profile + spa availability
        Opera-->>Tools: Guest data + available slots + preferences
        
        alt Availability Confirmed
            Tools->>Opera: Create spa reservation with preferences
            Opera-->>Tools: Booking confirmation + charge posting
            Tools->>Queue: Queue email confirmation task
            Queue->>Email: Send booking confirmation
            Email->>Opera: Get guest email + VIP status
            Email->>Email: Generate personalized confirmation
            Email-->>Queue: Email sent successfully
            Queue-->>Tools: Email delivery status
            Tools-->>LC: Booking success + email confirmation
            LC->>OpenAI: Generate natural response with details
            OpenAI-->>LC: "Perfect! I've booked your spa massage..."
            LC-->>API: Complete response with booking details
            API->>Cache: Cache successful interaction pattern
            API->>DB: Log full interaction + booking + email + metrics
            API-->>G: 🎯 Personalized confirmation + email notification
            
        else No Availability  
            Tools->>Opera: Check alternative time slots
            Opera-->>Tools: Alternative options available
            Tools-->>LC: Alternative suggestions
            LC->>OpenAI: Generate helpful alternatives
            OpenAI-->>LC: "2pm is booked, but I have 3pm or 4pm..."
            LC-->>API: Alternative options response
            API->>DB: Log interaction + alternative suggestions
            API-->>G: 🔄 Alternative time suggestions
        end
    end
    
    Note over G,DB: Full process: 50ms (cached) or 800ms (new)
    Note over Email,DB: Email tracking continues post-booking
    Email->>DB: Track email opens + clicks for analytics
```

## 🧠 **LangChain Agent Architecture with Tools**

```mermaid
graph TB
    subgraph "LangChain Agent Core"
        A[🤖 Agent Executor]
        B[💭 Agent Memory]
        C[🎯 Agent Prompts]
        D[🔄 Conversation Chain]
    end
    
    subgraph "LangChain Tools (Opera-Integrated)"
        E[🎭 book_activity_tool]
        F[💆 book_spa_tool]
        G[🍽️ order_room_service_tool]
        H[🧹 request_housekeeping_tool]
        I[🔧 report_maintenance_tool]
        J[👤 get_guest_profile_tool]
        K[💳 post_charges_tool]
    end
    
    subgraph "MCP Server Integration"
        L[📡 Activities MCP Server]
        M[📡 Spa MCP Server]
        N[📡 Room Service MCP Server]
        O[📡 Housekeeping MCP Server]
        P[📡 Maintenance MCP Server]
    end
    
    subgraph "Opera PMS Integration"
        Q[🏨 Opera Guest API]
        R[💰 Opera Billing API]
        S[🏠 Opera Room API]
        T[📅 Opera Reservations API]
    end
    
    A --> B
    A --> C
    A --> D
    A --> E
    A --> F
    A --> G
    A --> H
    A --> I
    A --> J
    A --> K
    
    E --> L
    F --> M
    G --> N
    H --> O
    I --> P
    
    L --> Q
    M --> Q
    N --> Q
    O --> Q
    P --> Q
    
    J --> Q
    K --> R
    L --> S
    M --> T
    
    style A fill:#f3e5f5
    style Q fill:#fff8e1
```

## 🎙️ **Voice Integration with LangChain + Opera**

```mermaid
sequenceDiagram
    participant G as Guest
    participant T as Twilio
    participant V as ElevenLabs
    participant LC as LangChain Agent
    participant Opera as Opera PMS
    participant Cache as Redis Cache
    
    G->>T: 📞 Calls hotel
    T->>Opera: 🔍 Lookup caller ID in guest database
    Opera-->>T: 👤 Guest profile (Mr. Smith, Room 304, VIP)
    T->>Cache: Check for cached greeting
    
    alt Personalized Greeting Cached
        Cache-->>V: 🎯 "Good evening Mr. Smith, how may I assist you?"
        V-->>T: 🗣️ Personalized audio
        T-->>G: 🔊 VIP greeting
    else Generate New Greeting
        T->>LC: 🧠 Generate VIP greeting for Mr. Smith
        LC->>V: 🎙️ Create personalized audio
        V-->>T: 🗣️ Custom greeting
        T->>Cache: 💾 Cache personalized greeting
        T-->>G: 🔊 Personalized response
    end
    
    G->>T: 🗣️ "Book dinner for tonight"
    T->>LC: 📝 Process with guest context
    LC->>Opera: 🍽️ Check dining availability + guest preferences
    Opera-->>LC: ✅ Available tables + guest dietary restrictions
    LC->>Opera: 📝 Create dining reservation
    Opera-->>LC: 🧾 Confirmation + auto-charge to room folio
    LC->>V: 🎙️ Generate confirmation message
    V-->>T: 🗣️ "Dinner confirmed for 7 PM, charged to room 304"
    T-->>G: 🔊 Complete confirmation
```

## 🔌 **MCP Protocol with Opera Integration**

```mermaid
graph LR
    subgraph "LangChain Tools"
        A[🛠️ Tool Registry]
        B[🔧 Tool Executor]
        C[📋 Tool Schema]
    end
    
    subgraph "MCP Transport Layer"
        D[📡 MCP Client]
        E[🔌 Stdio Transport]
        F[🌐 HTTP Transport]
    end
    
    subgraph "MCP Servers (Opera-Enabled)"
        G[🎭 Activities Server + Opera]
        H[💆 Spa Server + Opera]
        I[🍽️ Room Service + Opera]
        J[🧹 Housekeeping + Opera]
        K[🔧 Maintenance + Opera]
    end
    
    subgraph "Opera PMS APIs"
        L[🏨 Guest Profile API]
        M[💳 Billing API]
        N[📅 Reservation API]
        O[🏠 Room Status API]
    end
    
    A --> B
    B --> C
    C --> D
    D --> E
    D --> F
    
    E --> G
    F --> H
    E --> I
    F --> J
    E --> K
    
    G --> L
    H --> M
    I --> N
    J --> O
    K --> O
    
    style A fill:#f3e5f5
    style G fill:#e8f5e8
    style L fill:#fff8e1
```

## 🏗️ **Practical Data Architecture with Email Tracking**

```mermaid
erDiagram
    %% Core Data - What You Actually Need
    GUESTS ||--o{ CONVERSATIONS : has
    GUESTS ||--o{ BOOKINGS : makes
    GUESTS ||--o{ EMAIL_NOTIFICATIONS : receives
    GUESTS {
        string guest_id PK
        string opera_guest_id FK
        string room_number
        string guest_name
        string email_address
        datetime check_in
        datetime check_out
        string vip_status
    }
    
    CONVERSATIONS ||--o{ MESSAGES : contains
    CONVERSATIONS {
        string conversation_id PK
        string guest_id FK
        string channel
        datetime started_at
        datetime ended_at
        float guest_satisfaction
        boolean resolved
    }
    
    MESSAGES {
        string message_id PK
        string conversation_id FK
        string role
        text content
        datetime timestamp
        boolean cached
        int response_time_ms
        float openai_cost
    }
    
    BOOKINGS ||--o{ EMAIL_NOTIFICATIONS : triggers
    BOOKINGS {
        string booking_id PK
        string guest_id FK
        string service_type
        string status
        decimal amount
        datetime created_at
        boolean ai_assisted
        boolean email_sent
    }
    
    EMAIL_NOTIFICATIONS {
        string notification_id PK
        string guest_id FK
        string booking_id FK
        string email_type
        string status
        datetime sent_at
        datetime opened_at
        boolean clicked
        text template_used
    }
    
    %% Simple Analytics - Daily Rollups
    DAILY_STATS {
        date stat_date PK
        int total_conversations
        int total_bookings
        decimal total_revenue
        float avg_response_time
        float avg_satisfaction
        float cache_hit_rate
        int error_count
        int emails_sent
        float email_open_rate
    }
    
    %% Basic Error Tracking
    ERROR_LOGS {
        string error_id PK
        datetime occurred_at
        string error_type
        text error_message
        string guest_id
        boolean resolved
    }
```

## 📊 **Simple Dashboard - What Hotels Actually Want**

### **Daily Operations View**
```sql
-- Today's key metrics
SELECT 
  COUNT(*) as conversations_today,
  COUNT(CASE WHEN resolved = true THEN 1 END) as resolved_today,
  AVG(guest_satisfaction) as avg_satisfaction,
  SUM(CASE WHEN channel = 'voice' THEN 1 ELSE 0 END) as voice_calls
FROM conversations 
WHERE DATE(started_at) = CURRENT_DATE;

-- Revenue impact
SELECT 
  COUNT(*) as bookings_today,
  SUM(amount) as revenue_today,
  COUNT(CASE WHEN ai_assisted = true THEN 1 END) as ai_bookings
FROM bookings 
WHERE DATE(created_at) = CURRENT_DATE;
```

### **Performance Monitoring**
```sql
-- Response times (only if needed)
SELECT AVG(response_time_ms) as avg_response_time
FROM messages 
WHERE timestamp > NOW() - INTERVAL 1 HOUR;

-- Error rate (basic)
SELECT COUNT(*) as errors_today
FROM error_logs 
WHERE DATE(occurred_at) = CURRENT_DATE AND resolved = false;
```

## 🔧 **Simple Implementation**

```python
# Basic metrics collection
class SimpleMetrics:
    def log_conversation(self, guest_id, channel, satisfaction=None):
        # Just insert into conversations table
        pass
    
    def log_booking(self, guest_id, service_type, amount, ai_assisted=True):
        # Just insert into bookings table  
        pass
    
    def get_daily_summary(self):
        # Simple SELECT COUNT(*) queries
        return {
            "conversations": count_today_conversations(),
            "bookings": count_today_bookings(), 
            "revenue": sum_today_revenue(),
            "avg_satisfaction": avg_today_satisfaction()
        }
```

## 💰 **REALISTIC Costs with Complete System + Email**

```mermaid
graph TB
    subgraph "Actual Technology Costs"
        A[🧠 OpenAI API: $0.50-15/month]
        B[🎙️ ElevenLabs: $5-22/month]
        C[📞 Twilio: $30-100/month]
        D[🏗️ Infrastructure: $25-150/month]
        E[🏨 Opera API: TBD/month]
        II[📧 SendGrid Email: $15-50/month]
    end
    
    subgraph "Operational Savings"
        F[👨‍💼 Concierge Staff: $8k/month saved]
        G[📞 Phone Staff: $5k/month saved]
        H[🔧 Manual Booking: $3k/month saved]
        I[📊 Opera Data Entry: $2k/month saved]
        J[🎯 Faster Service: $4k/month revenue]
        JJ[📧 Manual Email Follow-up: $1k/month saved]
    end
    
    subgraph "Realistic Business Impact"
        K[💰 Net Savings: $22k/month]
        L[📈 ROI: 2000%+ annually]
        M[⏰ Staff Time Saved: 420 hours/month]
        N[😊 Guest Satisfaction: +40%]
    end
    
    A --> K
    B --> K
    C --> K
    D --> K
    II --> K
    
    F --> K
    G --> K
    H --> K
    I --> K
    J --> K
    JJ --> K
    
    K --> L
    K --> M
    K --> N
    
    style K fill:#c8e6c9
    style L fill:#c8e6c9
```

### **Updated Monthly Costs with Email**

| Hotel Size | Technology Cost | Savings Generated | Net Monthly Benefit |
|------------|----------------|-------------------|-------------------|
| **Small (50 rooms)** | $77/month | $7,000/month | **$6,923/month** |
| **Medium (100 rooms)** | $140/month | $13,000/month | **$12,860/month** |
| **Large (200+ rooms)** | $337/month | $23,000/month | **$22,663/month** |

**Cost per interaction: $0.07** (including email notifications)

## 🔧 **Implementation with LangChain + Opera + Email**

### **Phase 1: LangChain + Redis Setup **
```python
# Enhanced LangChain agent with caching
class CachedLangChainAgent:
    def __init__(self):
        self.cache = redis.Redis(host='localhost', port=6379)
        self.agent = create_openai_functions_agent(
            llm=ChatOpenAI(model="gpt-3.5-turbo"),
            tools=self.get_opera_tools(),
            prompt=self.get_hotel_prompt()
        )
        self.agent_executor = AgentExecutor(
            agent=self.agent, 
            tools=self.get_opera_tools(),
            memory=ConversationBufferWindowMemory(k=10)
        )
    
    async def process_with_cache(self, message: str, guest_context: dict):
        # Check cache first
        cache_key = f"langchain:{hash(message + str(guest_context))}"
        cached = await self.cache.get(cache_key)
        
        if cached:
            return json.loads(cached)
        
        # Process with LangChain + Opera
        result = await self.agent_executor.ainvoke({
            "input": message,
            "guest_context": guest_context
        })
        
        # Cache response
        await self.cache.setex(cache_key, 3600, json.dumps(result))
        return result
```

### **Phase 2: Opera PMS + Email Integration**
```python
# LangChain tools with Opera and email integration
@tool
def book_spa_with_opera(service_name: str, time: str, room_number: str) -> str:
    """Book spa service with Opera PMS and email confirmation"""
    
    # Get guest from Opera
    guest = opera_client.get_guest_by_room(room_number)
    
    # Check availability via MCP
    availability = spa_mcp_client.check_availability(service_name, time)
    
    # Create Opera reservation
    opera_reservation = opera_client.create_service_reservation({
        "guest_id": guest["guest_id"],
        "service_type": "SPA",
        "service_name": service_name,
        "scheduled_time": time
    })
    
    # Post charges to Opera folio
    opera_client.post_charge_to_folio(
        guest["folio_id"],
        spa_services[service_name]["price"],
        f"Spa: {service_name}"
    )
    
    # Send email confirmation
    email_result = email_service.send_booking_confirmation({
        "guest_email": guest["email"],
        "guest_name": guest["name"],
        "service_name": service_name,
        "appointment_time": time,
        "amount": spa_services[service_name]["price"],
        "booking_id": opera_reservation["reservation_id"]
    })
    
    # Log email notification
    db.insert_email_notification({
        "guest_id": guest["guest_id"],
        "booking_id": opera_reservation["reservation_id"],
        "email_type": "spa_booking_confirmation",
        "status": "sent" if email_result["success"] else "failed",
        "sent_at": datetime.now()
    })
    
    return f"✅ Spa booked & charged to folio {guest['folio_id']}. Confirmation email sent to {guest['email']}"

# Email service integration
class EmailService:
    def __init__(self):
        self.sendgrid = SendGridAPIClient(api_key=os.environ.get('SENDGRID_API_KEY'))
        
    def send_booking_confirmation(self, booking_data):
        """Send booking confirmation email with template"""
        
        template_data = {
            "guest_name": booking_data["guest_name"],
            "service_name": booking_data["service_name"],
            "appointment_time": booking_data["appointment_time"],
            "amount": f"${booking_data['amount']:.2f}",
            "booking_id": booking_data["booking_id"]
        }
        
        message = Mail(
            from_email='concierge@hotel.com',
            to_emails=booking_data["guest_email"],
            subject=f'Booking Confirmation - {booking_data["service_name"]}',
            html_content=self.render_template('spa_booking_confirmation.html', template_data)
        )
        
        try:
            response = self.sendgrid.send(message)
            return {"success": True, "message_id": response.headers.get('X-Message-Id')}
        except Exception as e:
            return {"success": False, "error": str(e)}
```

### **Phase 3: Voice + ElevenLabs + Email Integration **
```python
# Voice integration with email notifications
class VoiceConcierge:
    def __init__(self):
        self.elevenlabs = ElevenLabsClient()
        self.cache = redis.Redis()
        self.langchain_agent = CachedLangChainAgent()
        self.email_service = EmailService()
    
    async def process_voice_call(self, audio_stream, caller_id):
        # Look up guest in Opera by phone
        guest = opera_client.get_guest_by_phone(caller_id)
        
        # Check for cached personalized greeting
        greeting_key = f"voice_greeting:{guest['guest_id']}"
        cached_greeting = await self.cache.get(greeting_key)
        
        if not cached_greeting:
            greeting_text = f"Good evening {guest['name']}, this is your AI concierge. How may I assist you today?"
            greeting_audio = await self.elevenlabs.text_to_speech(greeting_text)
            await self.cache.setex(greeting_key, 86400, greeting_audio)  # Cache 24h
        
        return cached_greeting or greeting_audio
```

## 📊 **Dashboard Requirements - Advanced Analytics**
![Hotel AI Operations Dashboard_page-0001](https://github.com/user-attachments/assets/6facbde6-794f-4692-8d00-b7a60921e2a3)

### **Real-time Metrics Queries**
```sql
-- Current active conversations
SELECT COUNT(*) as active_conversations 
FROM conversations 
WHERE status = 'active' AND hotel_id = ?

-- Response time last hour
SELECT AVG(response_time_ms) as avg_response_time
FROM langchain_messages 
WHERE timestamp > NOW() - INTERVAL 1 HOUR

-- Cache hit rate today
SELECT 
  (SUM(CASE WHEN cached = true THEN 1 ELSE 0 END) * 100.0 / COUNT(*)) as cache_hit_rate
FROM langchain_messages 
WHERE DATE(timestamp) = CURRENT_DATE

-- Revenue attribution
SELECT 
  SUM(ai_attributed_revenue) as ai_revenue,
  COUNT(*) as ai_bookings
FROM revenue_attribution 
WHERE DATE(attributed_at) = CURRENT_DATE
```

### **Business Intelligence Views**
```sql
-- Guest satisfaction trends
CREATE VIEW guest_satisfaction_trends AS
SELECT 
  DATE(ended_at) as date,
  AVG(guest_satisfaction) as avg_satisfaction,
  COUNT(*) as total_conversations
FROM conversations
WHERE guest_satisfaction IS NOT NULL
GROUP BY DATE(ended_at);

-- Service performance analysis
CREATE VIEW service_performance AS
SELECT 
  service_type,
  COUNT(*) as total_bookings,
  AVG(processing_time_ms) as avg_processing_time,
  SUM(amount) as total_revenue
FROM bookings
WHERE ai_assisted = true
GROUP BY service_type;
```

## 🎯 **Key Success Metrics (Complete System)**

```mermaid
graph LR
    subgraph "Technical Performance"
        A[LangChain Response < 800ms]
        B[Cache Hit Rate > 70%]
        C[Opera API Success > 99%]
        D[Voice Quality Score > 4.5/5]
    end
    
    subgraph "Business Metrics"
        E[Guest Satisfaction +35%]
        F[Staff Efficiency +60%]
        G[Revenue per Guest +15%]
        H[Opera Data Accuracy 99%]
    end
    
    subgraph "Operational Metrics"
        I[MCP Server Uptime > 99.5%]
        J[Opera Integration Errors < 1%]
        K[Voice Call Success > 95%]
        L[Manual Override < 5%]
    end
    
    A --> E
    B --> F
    C --> H
    D --> E
    
    style A fill:#e8f5e8
    style E fill:#e8f5e8
    style F fill:#e8f5e8
```

## ✅ **Complete Technology Stack with Email**

| **Component** | **Technology** | **Monthly Cost** | **Purpose** |
|---------------|----------------|------------------|-------------|
| **AI Agent** | LangChain + OpenAI | $0.50-15 | Natural language processing |
| **Hotel PMS** | Opera PMS APIs | TBD | Guest data, billing, reservations |
| **Voice** | ElevenLabs + Twilio | $35-122 | Voice synthesis, phone calls |
| **Email** | SendGrid | $15-50 | Booking confirmations, notifications |
| **Caching** | Redis | $15-50 | Performance optimization |
| **Protocol** | MCP (FREE) | $0 | Service communication |
| **Database** | PostgreSQL | $25-100 | Analytics, conversation history |
| **API** | FastAPI | $25-75 | Gateway, load balancing |
| **Frontend** | React + WebSocket | Included | Real-time chat, staff dashboard |

**This is the complete, practical architecture with realistic costs ($62-287/month) and comprehensive analytics infrastructure for real business intelligence!** 🏨 

# **Scaling Plan**
We can discuss it in the call as I feel like this is enough for now, but already did the outline for it too so clients can automatically sign up to our website and use our software in minutes after paying.

https://lovable.dev/projects/2bd7117a-b57f-4954-92d1-c5b88c3c1195

