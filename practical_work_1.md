```mermaid
graph TD
    subgraph "Внешняя среда"
        U[Студент]
    end
    
    subgraph "Граница системы: Служба поддержки ИС"
        R[1. Регистрация обращения<br>created_at]
        Q[2. Очередь обращений]
        A[3. Назначение специалисту<br>assigned_at]
        P[4. Обработка и завершение<br>resolved_at]
    end
    
    subgraph "Управляемые ресурсы"
        S[Специалисты c_t]
    end

    U -->|Создает запрос| R
    R -->|request_id, Category| Q
    Q -->|Ожидание W_i| A
    S -->|Назначение specialist_id| A
    A --> P
    P -->|Status: закрыто| U

    %% Точки измерения KPI
    KPI((Измерение KPI:<br>Доля W_i ≤ 10 мин<br>и 90-й процентиль))
    Q -.-> KPI
    A -.-> KPI
    
    style KPI fill:#f9f,stroke:#333,stroke-width:2px
    style Q fill:#bbf,stroke:#333
