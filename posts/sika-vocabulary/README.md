# Sika Vocabulary

This is a collection of terms that are used across Sika and what they mean in the context of this program.

## People

| Term | Definition |
| --- | --- |
| **Learner** | Someone pursuing the goals of a program. Preferred to "student." |
| **Coach** | A staff member administering the program. Preferred to "teacher" or "instructor", as this relationship is collaborative rather than hierarchical. |

## Curriculum

| Term | Definition |
| --- | --- |
| **Program** | The top organizing level of curriculum. A program consists of units. |
| **Unit** | The second-highest organizing level of curriculum. A unit consists of sections and activities designed around a broad goal. |
| **Section** | The third-highest organizing level of curriculum. A section organizes activities around a narrow goal. |
| **Activity** | Readings, questions, and exercises used in the curriculum. |
| **Topic** | A reading focused around a narrow idea |
| **Concept** | A reading focused around a broad idea |
| **Guide** | Instructions for performing a task |
| **Prompt** | Question asked via the Inbox. |
| **Habit of Excellence** | A skill or behavior that's useful across many different disciplines. |

## Performances

| Term | Definition |
| --- | --- |
| **Performance** | A learner's engagement with an Activity or Prompt |
| **Submission** | A URL submitted as part of an Activity |
| **Response** | Text submitted as part of an Activity or Prompt |
| **View** | A performance for non-interactive content |
| **Confidence Level** | A self-rating of confidence for a View |
| **Evaluation** | A coach's response to a performance. May be accepted or rejected, and may optionally include comments. |
| **Accepted** | The performance was satisfactory and the learner can move on. Preferred to "passed" since there is no cut score that one is trying to pass. |
| **Rejected** | The performance was not satisfactory and the learner should try again. Preferred to "failed" since attempting something and learning from it is not a failure. |

## Instruction

| Term | Definition |
| --- | --- |
| **Lesson** | An interactive live session with learning objectives |
| **Study Hall** | An interactive live session driven by learner questions |
| **Demonstration** | A non-interactive live session driven by a coach |
| **1:1** | A private meeting between a learner and a coach |
| **Inbox** | A tool for real-time prompts and responses between coaches and learners |

## Technical

These are included for completeness, but are only relevant to working on this LMS software:

| Term | Definition |
| --- | --- |
| **Slug** | Unique identifier for posts |
| **Post** | Type containing the metadata and content for a unit of curriculum |
| **Raw Program** | A `.ts` file containing a hierarchy of posts. Must be processed to add paths. |
| **Dehydrated Program** | A `.json` file containing a raw program with paths added. Does not have content. Generated at build-time. |
| **Hydrated Program** | A file containing a dehydrated program with content fetched and added. Generated at run-time. |
| **Raw Performance** | A performance that has not been added to the database |
| **Posted Performance** | A performance that has been added to the database, and thus has an ID and timestamps |
| **Evaluated Performance** | A posted performance that has been evaluated by a coach |
| **Broadcast** | A prompt with associated metadata sent from an Inbox |
