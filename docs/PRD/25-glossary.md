25. Glossary

The following terminology should be used consistently throughout the LiftHub documentation and implementation.

Term	Definition

Member	An authenticated individual using LiftHub to track personal workouts.

Workout Template	A reusable workout plan consisting of a predefined sequence of exercises.

Workout Session	A completed or active workout performed by a Member.

Exercise	A predefined or custom movement performed during a workout.

Set	A single recorded performance of an exercise containing values such as weight and repetitions.

Personal Record (PR)	A Member's best recorded performance according to the application's defined criteria.

Workout History	The complete record of previous Workout Sessions.

Statistics	Aggregated metrics generated from Workout History, including workout frequency, total volume, exercise frequency, and streaks.

Exercise Library	The collection of available exercises that Members may use when creating Workout Templates or Workout Sessions.

Offline Mode	The ability to continue using LiftHub without an active internet connection while synchronizing changes when connectivity returns.

Synchronization	The process of reconciling locally stored data with Supabase once network connectivity becomes available.

Role	A logical permission group within LiftHub. V1 supports only the Member role, while Trainer and Gym Owner remain future roles.

Authentication	The process of verifying a Member's identity using supported sign-in methods.

Profile	The collection of personal preferences and fitness information associated with a Member account.

Design Impact:

This glossary serves as the authoritative source of terminology for all future documentation, database design, architecture, UI design, and implementation. New terminology should be introduced only when necessary and added here to maintain consistency across the project.

