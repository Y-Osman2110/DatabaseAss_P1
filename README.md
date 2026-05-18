# DatabaseAss_P1
This repo for solving database assignment Project 4: The Fitness Club & Personal Training Hub
			┌─────────────────────────────────────────────────────────────────────────────┐
			│                         GYM MANAGEMENT SYSTEM ERD                           │
			└─────────────────────────────────────────────────────────────────────────────┘

	┌───────────────────┐         ┌──────────────┐     
	│       Package     │         │ Subscription │         
	├───────────────────┤   M:1   ├──────────────┤         
	│ PK packId         │◄───┐    │ PK subscId   │   
	│    packName       │    └────│ FK packId    │   
	│    packCost       │    	  │ FK memberId  │
	│    packDuration   │     	  │    startDate │         
	│    packDescription│         │    endDate   │
	└───────────────────┘         │    status    │
                                  └──────────────┘
								          │  M:1
								          ▼ 
                   			      ┌──────────────────┐              ┌───────────────────┐
                        		  │       Member     │              │   HealthProfile   │
                       			  ├──────────────────┤      1:1     ├───────────────────┤
   ┌──────────────────────┐  	  │ PK memberId      │◄─ ─ ─ ─  ┐   │ PK HP_Id          │
   │        Trainer       │	      │    memberName    │   │      └ ─ ┤ FK memberId       │
   ├──────────────────────┤		  │    memberPhone   │   └────┐     │    HP_height      │
   │ PK trainerId         │	      │    memberEmail   │    1:M │     │    HP_weight      │
   │    trainerName       │	      │    memberAddress │        │     │    HP_age         │
   │    trainerSpecialty  │	      └──────────────────┘        │     │    HP_description │
   │    trainerDuration   │              │ 1:M                │     └───────────────────┘
   │    TDescription	  │              ▼                    │       ┌──────────────┐
   └──────────────────────┘      ┌──────────────┐			  │		  │   Check-in   │
                    │            │  Reservation │             │       ├──────────────┤
                    │            ├──────────────┤             │       │ PK checkId   │ 
                    │            │ PK reservId  │             └───────┤ FK memberId  │                                    
                    └───┐        │ FK memberId  │                     │    location  │
                        │        │ FK sessionId │                     │    timestamp │
                        │        │    reservDate│                     └──────────────┘
                        │        └──────────────┘
                        │              │ M:1
                    1:1 │              ▼
                        │      ┌────────────────────┐         ┌──────────────┐
                        │      │       Session      │         │     Zone     │
                        │      ├────────────────────┤  M:1    ├──────────────┤
                        │      │ PK sessionId       │    ┌────┤ Pk zoneNum   │
                        └──────┤ FK trainerId       │    │    │    location  │
						       │ FK zoneNum         │◄───┘    │    timestamp │
                               │    sessionName     │         └──────────────┘
                               │    discipline      │      
                               │    startTime       │         
                               │    endTime         │
                               │    sessionCapacity │
                               └────────────────────┘

═══════════════════════════════════════════════════════════════════════════════
                            RELATIONSHIP SUMMARY
═══════════════════════════════════════════════════════════════════════════════

    Package 1 ────────► M Subscription
    Subscription M ───► 1 Member
    Member 1 ─────────► 1 HealthProfile
    Member 1 ─────────► M Reservation
    Member 1 ─────────► M Check-in
    Reservation M ────► 1 Session
    Session M ────────► 1 Trainer
    Session M ────────► 1 Zone

═══════════════════════════════════════════════════════════════════════════════
                                 OVERVIEW
═══════════════════════════════════════════════════════════════════════════════
This document describes the Entity Relationship (ER) Diagram for a Gym Management System. The system manages gym members, trainers, packages, 
sessions, reservations, health profiles, and facility zones.

═══════════════════════════════════════════════════════════════════════════════
                                REQUIREMENTS
═══════════════════════════════════════════════════════════════════════════════
1. Functional Requirements:
The system must support the following core operations:
Member & Subscription Management: The system shall manage various tiered subscription packages and handle member enrollments.
Trainer Assignment: The system shall facilitate assigning members to specialized trainers for personalized, one-on-one coaching
Group Session Scheduling: The system shall create and manage schedules for group exercise sessions held in dedicated facility zones
Reservation Processing: The system shall allow members to reserve their spots for group exercise sessions in advance
Attendance Tracking: The system shall track every instance a member enters the facility (check-ins) to monitor peak usage times and
attendance patterns
Health Profile Updates: The system shall maintain and update member health-related data upon enrollment and during their membership

2. Data Requirements (Entities & Attributes):
Based on the Conceptual Model (ERD), the system must store the following data entities and their respective attributes:
Member: MemberID (PK), MemberName, MemberEmail, MemberPhone, and MemberAddress
Trainer: TrainerID (PK), TrainerName, TrainerSpecialty, TDescription, and TDuration
Package: PackID (PK), PackName, PackCost, PackDuration, and PackDescription
Session: SessionID (PK), SessionName, Discipline, StartTime, EndTime, and SessionCapacity
Zone: ZoneNum (PK), Location, and Timestamp
Health Profile: HP_Age, HP_Height, HP_Weight, and HP_Description
(Weak entity related to Member)
 Subscription: SubscriptionID (PK), StartDate, EndDate, and Status
 Reservation: ReservationID (PK) and ReservationDate
 Check-in: CheckinID (PK), Timestamp, and Location

2. Business Rules & Relationships

Member to Trainer: A member is assigned to one trainer for coaching, while a trainer can oversee several members (Many-to-One)
Member to Session: Members can reserve multiple sessions, and each session can have multiple member reservations (Many-to-Many)
Member to Subscription: A member can have multiple subscriptions over time, but each subscription belongs to one member
Session to Zone: Multiple sessions are held in one dedicated zone (Many-to-One)
Member to Health Profile: Each member has one unique health profile (One-to-One)
