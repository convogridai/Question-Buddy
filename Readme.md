# Welcome to Question Buddy!

Hey, we are building a Q&A application. The purpose of this application is simple. A user signs into the application and uploads a file containing questions. Then Question Buddy answers those questions. Question Buddy is very generous; it gives two answers for each question. But occasionally, it might fail to give an answer as well. 

## Anatomy of Question Buddy
Question Buddy consists of 4 main components. 

 - Buddy Frontend
 - Buddy Backend
 - Response Rover
 - IQ Buddy

###  Buddy Frontend 
This is the Gateway to Question Buddy. Users can log in to Buddy Frontend and upload a file with a list of questions that they would like to get answered. The question file follows the structure defined in the [Question Template](./sources/BuddyFrontend/question-template.json). Unless Question Buddy becomes unhappy and shows an error. Once a file is uploaded, all questions are visible to the user so that they can verify again. Once the user is confident about the questions, they can request the Question Buddy to go and fetch answers. Then Buddy Frontend sends a request to Buddy Backend to fetch answers. Once the answers are received, they are displayed to the user. When displaying the answers, Buddy Frontend makes sure to align answers with questions. When no answers are found Buddy Frontend humbly and sadly displays *I'm Sorry. No answers were found for your question*. Then user can sign out or upload another question file. 

###  Buddy Backend
Buddy Backend interacts with the Buddy Frontend. All requests from Buddy Frontend including authentication are handled by Buddy Backend. Buddy Backend tunnels most incoming requests to Response Rover and tries its best to answer all queries coming from the Buddy Frontend.


###  Response Rover
Response Rover is the microservice that resolves queries coming from the Buddy Backend. When Buddy Backend sends a question list, Response Rover sends those questions to IQ Buddy and sends the responses back. Response Rover has a well-defined [API specification](./sources/ResponseRover/openapi.yaml) and it works according to that. IQ Buddy sits behind an authentication layer so it's Response Rover's responsibility is to use proper credentials and get the job done. 


### IQ Buddy 
IQ Buddy is an application developed by another team and works as a web service. It exposes its capabilities via a set of well-defined APIs. Not much information about IQ Buddy is available except the published [API specification](./sources/IQBuddy/openapi.yaml). 

## A bit more about Question Buddy
Question Buddy is not just an answering machine. It tracks the following information as well.
 - For each user 
    - Question count
    - How many questions had two answers
    - How many questions had a single answer
    - How many questions without answers

- For each question list
    - How long does it take for the IQ Buddy to respond.
- Average time to answer a question.
- Number of `questions without answers` as a percentage of the overall question count.

None of the above information is exposed via Question Buddy. They are only stored for future reference.


## Bird's eye view of Question Buddy
![Bird's Eye View](./sources/QuestionBuddy.png)


## Here Comes the Challenge..
You are going to build the Question Buddy by implementing 
- Buddy Frontend
- Buddy Backend
- Response Rover

####  Buddy Frontend & Buddy Frontend
- This needs to be a NextJS (14) application. 
- Authentication must be handled within the NextJS application. 
- Buddy Backend should communicate with the Response Rover to get answers for user's questions. 
- Unfortunately, IQ Buddy is not very intelligent (yet). Most of the time, it says things that don't make any sense. However, that is not an issue for this task, as IQ Buddy provides a valid response.

####  Response Rover
- This needs to be a NodeJS project. 
- You have to implement the given [API specification](./sources/ResponseRover/openapi.yaml) properly. 
- The Response Rover doesn't need to be behind an authentication layer.
- The IQ Buddy host is https://iqbuddy.convogrid.ai. 
- The [API specification](./sources/IQBuddy/openapi.yaml) of IQ Buddy is publicly available. 
- Oauth client details will be shared with you separately. 

## Final Remarks
- Only MongoDB is permitted as the persistence layer.
- This is an open challenge with plenty of room for innovative thinking. 
- Make sure to read all sections carefully, as functional and non-functional requirements may be hidden in plain sight. 