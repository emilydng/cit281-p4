## Project 4

``` markdown
Goals and Outcomes

   - Gain experience interpreting functional descriptions and specifications to complete an assignment
  - Gain experience breaking a project into manageable components
  - Gain experience writing and executing non-web server Node.js JavaScript code using VSCode
  - Practice creating and using code modules
  - Practice using modern JavaScript syntax
  - Gain experience writing and executing Node.js REST API server using VSCode
  - Gain experience using Fastify with the GET verb, routes, and route parameters
  - Gain experience working with static data
  - Gain experience testing code module without using a web server
  - Gain experience using Postman to test web server routes
  - Gain experience working with JSON

```

p4-server.js

```rouge
  /*
    CIT 281 Project 4
    Name: Emily Deng
  */
  const p4 = require("./p4-module");
  const fastify = require("fastify")();

  // Route: /cit/question
  fastify.get("/cit/question", (request, reply) => {
      reply
        .code(200)
        .header("Content-Type", "application/json; charset=utf-8")
        .send(p4.getQuestions());
    });

  // Route: /cit/answer
  fastify.get("/cit/answer", (request, reply) => {
      reply
        .code(200)
        .header("Content-Type", "application/json; charset=utf-8")
        .send(p4.getAnswers());
    });

  // Route: /cit/questionanswer
  fastify.get("/cit/questionanswer", (request, reply) => {
      reply
        .code(200)
        .header("Content-Type", "application/json; charset=utf-8")
        .send(p4.getQuestionsAnswers());
    });

  // Route: /cit/question/:number
  fastify.get("/cit/question/:number", (request, reply) => {
      reply
        .code(200)
        .header("Content-Type", "application/json; charset=utf-8")
        .send(p4.getQuestion(request.params.number));
    });

  // Route: /cit/answer/:number
  fastify.get("/cit/answer/:number", (request, reply) => {
      reply
        .code(200)
        .header("Content-Type", "application/json; charset=utf-8")
        .send(p4.getAnswer(request.params.number));
    });

  // Route: /cit/questionanswer/:number
  fastify.get("/cit/questionanswer/:number", (request, reply) => {
      reply
        .code(200)
        .header("Content-Type", "application/json; charset=utf-8")
        .send(p4.getQuestionAnswer(request.params.number));
    });

  // Route: *
  fastify.get("*", (request, reply) => {
      reply
        .code(404)
        .header("Content-Type", "text/html; charset=utf-8")
        .send("<h1>Route not found</h1>");
    });

  // Extra Credit: Add support for POST
  fastify.post("/cit/students/add", (request, reply) => {
      let userData = JSON.parse(request.body)
      console.log(userData);
  });

  const listenIP = "localhost";
  const listenPort = 8080;
  fastify.listen(listenPort, listenIP, (err, address) => {
    if (err) {
      console.log(err);
      process.exit(1);
    }
    console.log(`Server listening on ${address}`);
  });
      CIT 281 Lab 1
      Name: Emily Deng
  */
  function square(num) {
      return num*num;
  }
  console.log('Square Operations: ')
  for (let i = 2; i <= 10; i+=2) {
      console.log(`Sqaure of ${i} is ${square(i)}`);
  }

  // right mouse click on file > open in integrated terminal

  ```
 
p4-module.js

```rouge
  const data = require('./p4-data');

  function addQuestionAnswer(info = {}) {

  }

  function getQuestions() {
      return data.data.map(x => x.question);
  }

  function getAnswers() {
      return data.data.map(x => x.answer);
  }

  function getQuestionsAnswers() {
      return data.data.slice(0);
  }

  function getQuestion(number = "") {
      if (isNaN(parseInt(number))) {
          return {
              error: 'Question number must be an integer',
              question: '',
              number: ''
          };
      }
      if (parseInt(number) > data.data.length) {
          return {
              error: 'Question number must be less than the number of questions (3)',
              question: '',
              number: ''
          };
      };
      if (parseInt(number) < 1) {
          return { 
              error: 'Question number must be >= 1', 
              question: '', 
              number: '' 
          };
      }
      const q = data.data.filter(x => x.question === 'Q' + number);
      if (q.length === 1) {
          return {
              error: '',
              question: q[0].question,
              number: q[0].question.substring(1)
          };
      }
  }
  
```
 
p4-data.js
 
 ```rouge
  // Question and answer data array
  const data = [
      {
        question: "Q1",
        answer: "A1",
      },
      {
        question: "Q2",
        answer: "A2",
      },
      {
        question: "Q3",
        answer: "A3",
      },
    ];

    // Export statement must be below data declaration - no hoisting with const
    module.exports = {
      data,
    };
    
  ```
