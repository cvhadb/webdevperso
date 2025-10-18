\## 2. Use Case Diagram

┌─────────────────────────────────────────────────────────────────┐
│ PLANNING TOOL SYSTEEM                                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ ┌─────────┐                                                     │
│ │ Manager │                                                     │
│ └────┬────┘                                                     │
│      │                                                          │
│      ├──► UC01: Teams en werknemers beheren                     │
│      ├──► UC02: Taken toewijzen en beheren                      │
│      ├──► UC03: Verlof goedkeuren/afwijzen                      │
│      ├──► UC04: Centraal planningsbord gebruiken                │
│      ├──► UC05: Vestigingen beheren                             │
│      ├──► UC06: Taken beheren                                   │
│      ├──► UC07: Werknemers beheren                              │
│      ├──► UC08: Dashboard met KPI's bekijken                    │
│      ├──► UC09: Plant details bekijken                          │
│      ├──► UC10: Notificaties bekijken                           │
│      ├──► UC11: Takenplanning per werknemer bekijken            │
│      └──► UC12: Taken herplannen bij afwezigheid                │  
│                                                                 │
│ ┌───────────┐                                                   │
│ │ Supervisor│                                                   │
│ └─────┬─────┘                                                   │
│       │                                                         │
│       ├──► UC09: Plant details bekijken                         │
│       ├──► UC08: Dashboard met KPI's bekijken                   │
│       ├──► UC13: Teamplanning bekijken                          │
│       ├──► UC14: Eigen planning bekijken                        │
│       ├──► UC15: Taken van team filteren/zoeken                 │
│       ├──► UC10: Notificaties bekijken                          │
│       ├──► UC05: Vestigingen beheren                            │
│       ├──► UC06: Taken beheren                                  │
│       └──► UC07: Werknemers beheren                             │
│                                                                 │
│ ┌──────────┐                                                    │
│ │Werknemer │                                                    │
│ └────┬─────┘                                                    │
│      │                                                          │
│      ├──► UC14: Eigen planning bekijken                         │
│      ├──► UC16: Taken overzicht bekijken                        │
│      ├──► UC17: Taken filteren/zoeken                           │
│      ├──► UC18: Taak markeren als voltooid                      │
│      ├──► UC19: Afwezigheid melden (ziekte)                     │
│      ├──► UC20: Verlof aanvragen                                │
│      ├──► UC21: Afwezigheden opvolgen en beheren                │
│      ├──► UC10: Notificaties bekijken                           │
│      └──► UC22: Chatbot raadplegen over taken (extra)           │
│                                                                 │
│ ┌─────────┐                                                     │
│ │ Systeem │ (automatisch - niet opgenomen in vpp)               │
│ └────┬────┘                                                     │
│      │                                                          │
│      ├──► UC23: Taken auto-dealloceren bij afwezigheid          │
│      ├──► UC24: Notificatie versturen bij planningswijziging    │
│      ├──► UC25: Notificatie versturen bij ziekte                │
│      └──► UC26: KPI's automatisch berekenen                     │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
