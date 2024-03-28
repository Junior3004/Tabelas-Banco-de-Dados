##################    BANCO DE DADOS GENERALISTA - (GENERALIST DATABASE)  ##################

# LISTA DE TABELAS DO BANCO DE DADOS - (LIST OF DATABASE TABLES )

Usuários (Users)
Permissões (Permissions)
Projetos (Projects)
Tarefas (Tasks)
Comentários (Comments)
Anexos (Attachments)
Histórico de atividades (Activity Log)
Configurações do Sistema (System Settings)
Logs de Erros (Error Logs)
Tags ou Categorias (Tags/Categories)
Clientes (Clients)
Funcionários (Employees)
Fornecedores (Suppliers)
Inventário (Inventory)
Pedidos (Orders)
Pagamentos (Payments)
Calendário (Calendar)
Localizações (Locations)
Notificações (Notifications)
Feedback (Feedback)
Agenda de Contatos (Contacts)
Eventos (Events)
Recursos (Resources)
Categorias de Produtos (Product Categories)
Logs de Acesso (Access Logs)
Interações de Usuários (User Interactions)
Avaliações (Reviews)
Histórico de Preços (Price History)
Documentos (Documents)
Notas (Notes)
Questionários (Surveys)
Respostas (Responses)
Assinaturas (Subscriptions)
Problemas (Issues)
Metas (Goals)
Histórico de Versões (Version History)
Registros de Auditoria (Audit Logs)
Campanhas de Marketing (Marketing Campaigns)
Histórico de Transações (Transaction History)
Recursos Humanos (Human Resources)

------------------------------------------------------------------------------------------------------------------
# CODIGOS SQL ( SQL CODES )
------------------------------------------------------------------------------------------------------------------

Usuários (Users)

CREATE TABLE Users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);


------------------------------------------------------------------------------------------------------------------

Permissões (Permissions):

CREATE TABLE Permissions (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Projetos (Projects):

CREATE TABLE Projects (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    start_date DATE,
    end_date DATE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Tarefas (Tasks):

CREATE TABLE Tasks (
    id INT AUTO_INCREMENT PRIMARY KEY,
    project_id INT NOT NULL,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    status ENUM('todo', 'in_progress', 'completed') DEFAULT 'todo',
    priority ENUM('low', 'medium', 'high') DEFAULT 'medium',
    due_date DATE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (project_id) REFERENCES Projects(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------  

Comentários (Comments):

CREATE TABLE Comments (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    project_id INT NOT NULL,
    comment TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(id) ON DELETE CASCADE,
    FOREIGN KEY (project_id) REFERENCES Projects(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------ 

Anexos (Attachments):

CREATE TABLE Attachments (
    id INT AUTO_INCREMENT PRIMARY KEY,
    task_id INT NOT NULL,
    filename VARCHAR(255) NOT NULL,
    filepath VARCHAR(255) NOT NULL,
    uploaded_by INT NOT NULL,
    uploaded_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (task_id) REFERENCES Tasks(id) ON DELETE CASCADE,
    FOREIGN KEY (uploaded_by) REFERENCES Users(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------

Histórico de atividades (Activity Log):

CREATE TABLE ActivityLog (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    action VARCHAR(100) NOT NULL,
    details TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------

Configurações do Sistema (System Settings):

CREATE TABLE SystemSettings (
    id INT AUTO_INCREMENT PRIMARY KEY,
    setting_key VARCHAR(100) NOT NULL,
    setting_value TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Logs de Erros (Error Logs):

CREATE TABLE ErrorLogs (
    id INT AUTO_INCREMENT PRIMARY KEY,
    error_message TEXT NOT NULL,
    error_code INT,
    occurred_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Tags ou Categorias (Tags/Categories):

CREATE TABLE Tags (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Clientes (Clients):

CREATE TABLE Clients (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100),
    phone VARCHAR(20),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Funcionários (Employees):

CREATE TABLE Employees (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100),
    phone VARCHAR(20),
    department VARCHAR(100),
    hire_date DATE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Fornecedores (Suppliers):

CREATE TABLE Suppliers (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    contact_name VARCHAR(100),
    email VARCHAR(100),
    phone VARCHAR(20),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Inventário (Inventory):

CREATE TABLE Inventory (
    id INT AUTO_INCREMENT PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    description TEXT,
    quantity INT,
    price DECIMAL(10, 2),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Pedidos (Orders):

CREATE TABLE Orders (
    id INT AUTO_INCREMENT PRIMARY KEY,
    customer_id INT NOT NULL,
    order_date DATE,
    total_amount DECIMAL(10, 2),
    status ENUM('pending', 'processing', 'shipped', 'delivered') DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (customer_id) REFERENCES Customers(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------

Pagamentos (Payments):

CREATE TABLE Payments (
    id INT AUTO_INCREMENT PRIMARY KEY,
    order_id INT NOT NULL,
    payment_date DATE,
    amount DECIMAL(10, 2),
    payment_method VARCHAR(100),
    status ENUM('pending', 'completed', 'failed') DEFAULT 'pending',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (order_id) REFERENCES Orders(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------

Calendário (Calendar):

CREATE TABLE Calendar (
    id INT AUTO_INCREMENT PRIMARY KEY,
    event_name VARCHAR(100) NOT NULL,
    event_date DATE,
    event_time TIME,
    location VARCHAR(100),
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Localizações (Locations):

CREATE TABLE Locations (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    address VARCHAR(255),
    city VARCHAR(100),
    state VARCHAR(100),
    country VARCHAR(100),
    zip_code VARCHAR(20),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Notificações (Notifications):

CREATE TABLE Notifications (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    message TEXT NOT NULL,
    is_read BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------

Feedback (Feedback):

CREATE TABLE Feedback (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    feedback_type ENUM('positive', 'negative', 'neutral') NOT NULL,
    comment TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------

Agenda de Contatos (Contacts):

CREATE TABLE Contacts (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100),
    phone VARCHAR(20),
    address VARCHAR(255),
    notes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Eventos (Events):

CREATE TABLE Events (
    id INT AUTO_INCREMENT PRIMARY KEY,
    event_name VARCHAR(100) NOT NULL,
    event_date DATE,
    start_time TIME,
    end_time TIME,
    location VARCHAR(255),
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Recursos (Resources):

CREATE TABLE Resources (
    id INT AUTO_INCREMENT PRIMARY KEY,
    resource_name VARCHAR(100) NOT NULL,
    resource_type ENUM('room', 'equipment', 'vehicle', 'other') NOT NULL,
    location VARCHAR(255),
    capacity INT,
    status ENUM('available', 'booked', 'maintenance') DEFAULT 'available',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Categorias de Produtos (Product Categories):

CREATE TABLE ProductCategories (
    id INT AUTO_INCREMENT PRIMARY KEY,
    category_name VARCHAR(100) NOT NULL,
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Logs de Acesso (Access Logs):

CREATE TABLE AccessLogs (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    access_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    ip_address VARCHAR(50),
    user_agent VARCHAR(255),
    status ENUM('success', 'failed') DEFAULT 'success'
);

------------------------------------------------------------------------------------------------------------------

Interações de Usuários (User Interactions):

CREATE TABLE UserInteractions (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    action VARCHAR(100) NOT NULL,
    target_id INT,
    interaction_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------

Avaliações (Reviews):

CREATE TABLE Reviews (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    rating INT NOT NULL,
    review_text TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------

Histórico de Preços (Price History):

CREATE TABLE PriceHistory (
    id INT AUTO_INCREMENT PRIMARY KEY,
    product_id INT NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    effective_date DATE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (product_id) REFERENCES Products(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------

Documentos (Documents):

CREATE TABLE Documents (
    id INT AUTO_INCREMENT PRIMARY KEY,
    document_name VARCHAR(255) NOT NULL,
    document_type ENUM('pdf', 'docx', 'xlsx', 'jpg', 'png', 'other') NOT NULL,
    document_path VARCHAR(255) NOT NULL,
    uploaded_by INT NOT NULL,
    uploaded_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (uploaded_by) REFERENCES Users(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------

Notas (Notes):

CREATE TABLE Notes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    note_title VARCHAR(255),
    note_content TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------

Questionários (Surveys):

CREATE TABLE Surveys (
    id INT AUTO_INCREMENT PRIMARY KEY,
    survey_name VARCHAR(100) NOT NULL,
    description TEXT,
    created_by INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (created_by) REFERENCES Users(id) ON DELETE SET NULL
);

------------------------------------------------------------------------------------------------------------------

Respostas (Responses):

CREATE TABLE Responses (
    id INT AUTO_INCREMENT PRIMARY KEY,
    survey_id INT NOT NULL,
    respondent_id INT NOT NULL,
    response TEXT,
    response_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (survey_id) REFERENCES Surveys(id) ON DELETE CASCADE,
    FOREIGN KEY (respondent_id) REFERENCES Users(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------

Assinaturas (Subscriptions):

CREATE TABLE Subscriptions (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    subscription_plan VARCHAR(100) NOT NULL,
    start_date DATE NOT NULL,
    end_date DATE,
    status ENUM('active', 'cancelled', 'paused') DEFAULT 'active',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------

Problemas (Issues):

CREATE TABLE Issues (
    id INT AUTO_INCREMENT PRIMARY KEY,
    project_id INT NOT NULL,
    title VARCHAR(255) NOT NULL,
    description TEXT,
    status ENUM('open', 'closed', 'in_progress') DEFAULT 'open',
    priority ENUM('low', 'medium', 'high') DEFAULT 'medium',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (project_id) REFERENCES Projects(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------

Metas (Goals):

CREATE TABLE Goals (
    id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT NOT NULL,
    goal_name VARCHAR(255) NOT NULL,
    description TEXT,
    target_date DATE,
    achieved BOOLEAN DEFAULT FALSE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES Users(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------

Histórico de Versões (Version History):

CREATE TABLE VersionHistory (
    id INT AUTO_INCREMENT PRIMARY KEY,
    software_name VARCHAR(100) NOT NULL,
    version_number VARCHAR(20) NOT NULL,
    release_date DATE,
    changes TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Registros de Auditoria (Audit Logs):

CREATE TABLE AuditLogs (
    id INT AUTO_INCREMENT PRIMARY KEY,
    action VARCHAR(255) NOT NULL,
    performed_by INT NOT NULL,
    performed_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (performed_by) REFERENCES Users(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------

Campanhas de Marketing (Marketing Campaigns):

CREATE TABLE MarketingCampaigns (
    id INT AUTO_INCREMENT PRIMARY KEY,
    campaign_name VARCHAR(255) NOT NULL,
    description TEXT,
    start_date DATE,
    end_date DATE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Histórico de Transações (Transaction History):

CREATE TABLE TransactionHistory (
    id INT AUTO_INCREMENT PRIMARY KEY,
    transaction_type ENUM('purchase', 'sale') NOT NULL,
    transaction_date DATE,
    amount DECIMAL(10, 2) NOT NULL,
    details TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

------------------------------------------------------------------------------------------------------------------

Recursos Humanos (Human Resources):

CREATE TABLE HumanResources (
    id INT AUTO_INCREMENT PRIMARY KEY,
    employee_id INT NOT NULL,
    department VARCHAR(100),
    job_title VARCHAR(100),
    salary DECIMAL(10, 2),
    start_date DATE,
    end_date DATE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (employee_id) REFERENCES Employees(id) ON DELETE CASCADE
);

------------------------------------------------------------------------------------------------------------------
