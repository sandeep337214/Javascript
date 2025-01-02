<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="/todolist.css" />
  </head>
  <body>
    <h1>Todo List</h1>
    <br />
    <form>
      <div>
        <input type="text" id="inputValue" />
        <button class="btn">Add Todo</button>
      </div>
      <section class="todo-list-elem"></section>
    </form>

    <script>
      const MaintodoElem = document.querySelector(".todo-list-elem");
      const inputValue = document.getElementById("inputValue");

      const getTodoKListFromLocal = () => {
        return JSON.parse(localStorage.getItem("youtubeTodo"));
      };

      const addtodolistlocalStorage=(localTodoLists)=>{
        return localStorage.setItem("youtubeTodo", JSON.stringify(localTodoLists));
      }


      let localTodoLists = getTodoKListFromLocal() || [];
      addTododynamicelement = (element) => {
        const divElement = document.createElement("div");
        divElement.classList.add("main_todo_div");
        divElement.innerHTML = `<li>${element}</li><button class="deletebtn">Delete</button>`;
        MaintodoElem.append(divElement);
      };

      const addTodoList = (e) => {
        e.preventDefault();

        const todoListvalue = inputValue.value.trim();
        inputValue.value = "";
        if (!localTodoLists.includes(todoListvalue) && todoListvalue != "") {
          localTodoLists.push(todoListvalue);
          localTodoLists = [...new Set(localTodoLists)];
          localStorage.setItem("youtubeTodo", JSON.stringify(localTodoLists));
          console.log(localTodoLists);

          addTododynamicelement(todoListvalue);
        }
      };
      const Showtodos = () => {
        localTodoLists.forEach((element) => {
          addTododynamicelement(element);
        });
      };
      Showtodos();

      const removeTodoElem=(e)=>{
        
        const todoremove=e.target;
        let todolistcontent = todoremove.previousElementSibling.innerText;
        let parentElem=todoremove.parentElement;
        console.log(todolistcontent);

        localTodoLists =localTodoLists.filter((curtodo)=>{
          // console.log(curtodo);
          
          return curtodo!=todolistcontent.toLowerCase();
        })

        addtodolistlocalStorage(localTodoLists);
        parentElem.remove();
        console.log(localTodoLists);
        
      }
      MaintodoElem.addEventListener("click", (e) => {
        e.preventDefault();
        
        if(e.target.classList.contains('deletebtn')){
          removeTodoElem(e);
        }
      });
      document.querySelector(".btn").addEventListener("click", (e) => {
        
        
        addTodoList(e);
      });
    </script>
  </body>
</html>
body{
    background-color: black;
    width: 100%;
    height: 90vh;

}
.btn{
    font-family: sans-serif;
    font-size: 15px;
    font-weight: bold;
    width: 150px;
    height: 30px;
    background-color: rgb(226, 216, 30);
    border-radius: 20px;
    border: none;
    cursor: pointer;
}
input{
    border: none;
    border-radius: 3px;
    width: 250px;
    height: 26px;
}

h1{
    color: white;
    font-family: sans-serif;
    font-weight: bold;
    margin-left: 300px;
    
}
div{
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
    margin-bottom: 30px;
}
li{
    font-family: sans-serif;
    font-size: 15px;
    font-weight: bold;
    width: 150px;
    height: 30px;
    color: white;
    border-radius: 20px;
    border: none;
    position: relative;
    right: 30px;
}   
.deletebtn{
    font-family: sans-serif;
    font-size: 15px;
    font-weight: bold;
    width: 150px;
    height: 30px;
    background-color: rgb(226, 216, 30);
    border-radius: 20px;
    border: none;
    cursor: pointer;
}
.deletebtn:hover{
    background-color: rgb(232, 232, 232);
    border: 3px solid rgb(226, 216, 30);
    
}
.todo-lists-elem{
    margin-top:30px;
    display: flex;
    flex-direction: column;
    gap: 10px;
    position: relative;
    right: 20px;
}
