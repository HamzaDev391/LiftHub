21. Dependencies

LiftHub V1 depends on several external services, platforms, and internal project deliverables.

21.1 External Dependencies

ID	Dependency	Purpose

D-01	Supabase Auth	User authentication and session management.
D-02	Supabase PostgreSQL	Persistent relational data storage.
D-03	Supabase Storage	Future support for user-uploaded assets if required.
D-04	Flutter	Cross-platform mobile application framework.
D-05	iOS and Android operating systems	Application runtime environments.

21.2 Internal Project Dependencies

ID	Dependency	Purpose

D-06	Product Requirements Document	This document serves as the authoritative product specification.
D-07	Entity Relationship Diagram (ERD)	Defines the relational database model.
D-08	System Architecture	Document describing application layers, synchronization, repositories, and service boundaries.
D-09	UI/UX Design	Systematic screen layouts, navigation, and visual design.
D-10	Testing Strategy	Defines unit, integration, widget, and manual testing approaches.

21.3 Dependency Principles

• Business rules originate from this PRD.

• The ERD must implement the business rules defined here.

• Architecture must implement the ERD.

• Flutter implementation must follow the architecture.

• Changes should flow downward through the documentation hierarchy rather than directly into implementation.

Design Impact:
This dependency order minimizes conflicting requirements and keeps implementation aligned with documented product decisions.

