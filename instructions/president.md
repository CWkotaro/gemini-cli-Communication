# 👑 PRESIDENT'S BRIEFING

## Your Role
As the Project Owner, your role is to initiate the project by providing a clear, high-level objective. You will start the entire multi-agent workflow by creating a single file.

## Your ONE and ONLY Action
To start the project, create a file named `request.txt` inside the `tmp` directory. The content of this file will be your high-level instruction to the `boss` agent.

### How to Start the Project (Example)

Use the following command in your **own terminal** (the one you are using to interact with the agents) to create the request file.

**Example 1: Create a simple "Hello World" website**
```bash
echo "Create a simple 'Hello World' website in a project folder named 'hello-world-site'." > ./tmp/request.txt
```

**Example 2: Develop a REST API for a to-do list**
```bash
echo "Develop a REST API for a to-do list. The project folder should be 'todo-api'." > ./tmp/request.txt
```

## What Happens Next?
1.  The `boss` agent will automatically detect this new new file.
2.  It will read your request, create a project plan, and assign specific tasks to the `worker` agents.
3.  The `boss` will then delete `tmp/request.txt` to confirm it has accepted the task.
4.  You can monitor the progress by observing the files appearing in the `tmp` directory and the project folder.

## Monitoring the Project
- **Project Plan:** The `boss` will create a `MASTER_TASKS.md` file in the project's root directory (e.g., `/workspace/hello-world-site/MASTER_TASKS.md`).
- **Final Report:** Once the entire project is complete, the `boss` will create a `final_report.txt` file in the `tmp` directory. You can view this file to see the results.

```bash
# To check the final report
cat ./tmp/final_report.txt
```

**Your turn. Please provide your instruction by creating the `tmp/request.txt` file.**