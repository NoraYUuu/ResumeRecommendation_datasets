# ResumeRecommendation_datasets
This repository contains the human annotation dataset collected using the Feedback-Enhanced Resume Recommender (FERR) model.

Please refer to `table_relation.png` to understand the relationships among these tables. For anonymity reasons, the `user` table and `user_status` table have been removed. Additionally, the `date` column in the interaction tables has been removed. This removal will not affect the table content as these tables and columns are used internally to ensure system consistency.

## Table Relation
![Table Relationships](table_relation.png)

## Database schema
### User Table

The HR table stores information about HR professionals or users who provide feedback and interact with the system. Each HR user is assigned a unique identifier (ID), which is crucial for tracking their activities and managing their data.

- **ID**: Unique identifier for HR user. Auto-increment.
- **userName**: User name used when sign up and log in.

### Feedback Interaction Table

This table captures the interactions between HR users and the system during feedback sessions. It includes details such as the HR ID, JD ID (Job Description ID), résumé ID, feedback provided by the HR user, validation status of the feedback, and timestamps.

- **HR-ID**: Foreign key referencing HR Table.
- **JD-ID**: Foreign key referencing Job Description Table.
- **resume-ID**: Unique identifier for the résumé.
- **Feedback**: Feedback provided by HR user.
- **IsChosen**: Indicator if the résumé is deemed good/better than the previous one.
- **Validation**: Validation question answer of the feedback.
- **date**: Timestamp of the interaction.

### Models Table

The models table stores information about different models used within the system.

- **Model Index**: Unique identifier for the model.
- **Model Name**: Name of the model.

### Model Recommendation Table

This table records the recommendations generated by models based on HR feedback and system algorithms.

- **Model Index**: Foreign key referencing Models Table.
- **JD-ID**: Foreign key referencing Job Description Table.
- **Rank**: Rank of the recommendation.
- **resume-ID**: Unique identifier for the résumé.
- **Sequence**: Sequence order of recommendations. This sequence is used because the annotation stage is shuffled to ensure blindness.
- **HR-ID**: Foreign key referencing HR Table.

### Label Interaction Table

The label interaction table stores information related to label scoring and relevance assessment.

- **HR-ID**: Foreign key referencing HR Table.
- **JD-ID**: Foreign key referencing Job Description Table.
- **resume-ID**: Unique identifier for the résumé.
- **Relevant Score**: Score indicating relevance of a résumé.
- **date**: Timestamp of the interaction.

### User Status Table

The user status table tracks and manages the status of users within the system. Used to decide which page to direct this user to.

- **User ID**: Unique identifier for the user.
- **Status**: Current status of the user.
- **date**: Timestamp of status updates.

The Feedback Interaction and Label Interaction tables play a crucial role in collecting and storing data related to HR feedback and label scoring. The data stored in these tables are later used for experiments. In contrast, the other tables, such as User, Models, Model Recommendation, and User Status, facilitate the functionality of the website and manage system operations without directly capturing user-generated data.
