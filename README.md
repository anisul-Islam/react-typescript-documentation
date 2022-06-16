# React + Typescript documentation

- prerequisities - TypeScript, React Fundamentals

## 1. Introduction to TypeScript

- What is TypeScript?

  - programming language developed by microsoft
  - superset of JavaScript

- Why TypeScript?

  - adds static typing to JavaScript
  - it helps to see bugs when writing codes; easy to find and fix bugs
  - gives auto suggestion
  - provides better documentation

- Course outcomes
  - props types
    - built-in data type props
    - user defined data type props
    - events props
  - hooks types

## 2. Environment setup

- install node & VSCode
- install react+ts -> `npx create-react-app appName --template typescript`

## 3. typescript for Props - built in types

- built in types example -> string, number, boolean
- extension .ts and component extension is .tsx not .js or .jsx

```tsx
// auto completion -> props.
// if we pass anything other than string as name props we will get error
// component props is an object
// User.tsx (version-1)
import React from "react";
const User = (props: {
  name: string;
  email: string;
  age: number;
  isRegistered: boolean;
}) => {
  return (
    <div style={{ border: "1px solid", margin: "1rem" }}>
      <h2>{props.name}</h2>
      <p>{props.email}</p>
      <p>{props.age} years old</p>
      {props.isRegistered ? (
        <p>Registered Student</p>
      ) : (
        <p>Unregistered Student</p>
      )}
    </div>
  );
};

export default User;

// User.tsx (version-2)
import React from "react";

type UserProps = {
  name: string;
  email: string;
  age: number;
  isRegistered: boolean;
};
const User = (props: UserProps) => {
  return (
    <div style={{ border: "1px solid", margin: "1rem" }}>
      <h2>{props.name}</h2>
      <p>{props.email}</p>
      <p>{props.age} years old</p>
      {props.isRegistered ? (
        <p>Registered Student</p>
      ) : (
        <p>Unregistered Student</p>
      )}
    </div>
  );
};
export default User;

// User.tsx (version-3)
import React from "react";
type UserProps = {
  name: string;
  email: string;
  age: number;
  isRegistered: boolean;
};
const User = ({ name, email, age, isRegistered }: UserProps) => {
  return (
    <div style={{ border: "1px solid", margin: "1rem" }}>
      <h2>{name}</h2>
      <p>{email}</p>
      <p>{age} years old</p>
      {isRegistered ? <p>Registered Student</p> : <p>Unregistered Student</p>}
    </div>
  );
};
export default User;

// App.tsx
import React from "react";
import "./App.css";
import User from "./components/User";

function App() {
  return (
    <div className="App">
      <h1>User Management App</h1>
      <User
        name="anisul islam"
        email="anisul2010s@yahoo.co.uk"
        age={32}
        isRegistered={true}
      />
      <User
        name="Rabeya Begum"
        email="rabu2010s@yahoo.co.uk"
        age={31}
        isRegistered={false}
      />
    </div>
  );
}

export default App;

// void
const handleClick = (): void => {
  console.log("clicked");
};
```

## 4. typescript for Props - User defined types

- Object, Array, Union, enum, tuple, any, custom type

- object props

  ```tsx
  import React from "react";

  type UserProps = {
    user: {
      name: string;
      email: string;
      age: number;
      isRegistered: boolean;
    };
  };
  const User = ({ user }: UserProps) => {
    return (
      <div style={{ border: "1px solid", margin: "1rem" }}>
        <h2>{user.name}</h2>
        <p>{user.email}</p>
        <p>{user.age} years old</p>
        {user.isRegistered ? (
          <p>Registered Student</p>
        ) : (
          <p>Unregistered Student</p>
        )}
      </div>
    );
  };

  export default User;

  // App.tsx
  import React from "react";
  import "./App.css";
  import User from "./components/User";

  const user1 = {
    name: "anisul islam",
    email: "anisul2010s@yahoo.co.uk",
    age: 32,
    isRegistered: true,
  };
  const user2 = {
    name: "Rabeya Begum",
    email: "rabu2010s@yahoo.co.uk",
    age: 31,
    isRegistered: false,
  };

  function App() {
    return (
      <div className="App">
        <h1>User Management App</h1>
        <User user={user1} />
        <User user={user2} />
      </div>
    );
  }

  export default App;

  // more updates for App.tsx
  import React from "react";
  import "./App.css";
  import User from "./components/User";

  const users = [
    {
      id: 1,
      name: "anisul islam",
      email: "anisul2010s@yahoo.co.uk",
      age: 32,
      isRegistered: true,
    },
    {
      id: 2,
      name: "Rabeya Begum",
      email: "rabu2010s@yahoo.co.uk",
      age: 31,
      isRegistered: false,
    },
  ];

  function App() {
    return (
      <div className="App">
        <h1>User Management App</h1>
        {users.map((user) => (
          <User key={user.id} user={user} />
        ))}
      </div>
    );
  }

  export default App;
  ```

- array props

  ```tsx
  // simple example
  import React from "react";

  type UserProps = {
    lang: string[];
  };
  const User = ({ lang }: UserProps) => {
    return (
      <div style={{ border: "1px solid", margin: "1rem" }}>
        <p>
          Speaks:{" "}
          {lang.map((language, index) => {
            return <span key={index}>{language} </span>;
          })}
        </p>
      </div>
    );
  };
  export default User;

  // App.tsx
  import React from "react";
  import "./App.css";
  import User from "./components/User";
  function App() {
    return (
      <div className="App">
        <h1>User Management App</h1>
        <User lang={["Bangla", "English", "Finnish"]} />
      </div>
    );
  }
  export default App;

  // complex example
  import React from "react";

  type UserProps = {
    user: {
      name: string;
      email: string;
      age: number;
      isRegistered: boolean;
      languages: string[];
    };
  };
  const User = ({ user }: UserProps) => {
    return (
      <div style={{ border: "1px solid", margin: "1rem" }}>
        <h2>{user.name}</h2>
        <p>{user.email}</p>
        <p>{user.age} years old</p>
        {user.isRegistered ? (
          <p>Registered Student</p>
        ) : (
          <p>Unregistered Student</p>
        )}
        <p>
          Speaks:{" "}
          {user.languages.map((language, index) => {
            return <span key={index}>{language} </span>;
          })}
        </p>
      </div>
    );
  };
  export default User;

  // App.tsx
  import React from "react";
  import "./App.css";
  import User from "./components/User";

  const users = [
    {
      id: 1,
      name: "anisul islam",
      email: "anisul2010s@yahoo.co.uk",
      age: 32,
      isRegistered: true,
      languages: ["Bangla", "English"],
    },
    {
      id: 2,
      name: "Rabeya Begum",
      email: "rabu2010s@yahoo.co.uk",
      age: 31,
      isRegistered: false,
      languages: ["Bangla", "English", "Finnish"],
    },
  ];

  function App() {
    return (
      <div className="App">
        <h1>User Management App</h1>
        {users.map((user) => (
          <User key={user.id} user={user} />
        ))}
      </div>
    );
  }
  export default App;

  // one more array example

  // App.tsx
  import React from "react";
  import "./App.css";
  import User from "./components/User";
  const users = [
    {
      id: 1,
      name: "anisul islam",
      email: "anisul2010s@yahoo.co.uk",
    },
    {
      id: 2,
      name: "Rabeya Begum",
      email: "rabu2010s@yahoo.co.uk",
    },
  ];

  function App() {
    return (
      <div className="App">
        <h1>User Management App</h1>
        <User users={users} />
      </div>
    );
  }
  export default App;

  // User.tsx
  import React from "react";
  type UserProps = {
    users: {
      id: number;
      name: string;
      email: string;
    }[];
  };
  const User = ({ users }: UserProps) => {
    return (
      <div>
        {users.map((user) => {
          const { id, name, email } = user;
          return (
            <div key={id} style={{ border: "1px solid", margin: "1rem" }}>
              <p>{name}</p>
              <p>{email}</p>
            </div>
          );
        })}
      </div>
    );
  };
  export default User;
  ```

- union of types

  ```tsx
  // Message.tsx
  import React from "react";

  type MessageProps = {
    text: "ADD" | "UPDATE" | "DELETE";
  };

  const Message = (props: MessageProps) => {
    if (props.text === "ADD") {
      return <p>User is added</p>;
    } else if (props.text === "UPDATE") {
      return <p>User is updated</p>;
    }
    return <p>User is deleted</p>;
  };

  export default Message;

  // App.tsx
  function App() {
    return (
      <div className="App">
        <h1>User Management App</h1>
        <Message text="UPDATE" />
        {/* <User users={users} /> */}
      </div>
    );
  }

  export default App;
  ```

- children props

  ```tsx
  // Card.tsx
  import React from "react";
  type CardProps = {
    children: React.ReactNode;
  };
  const Card = (props: CardProps) => {
    return <div className="card">{props.children}</div>;
  };

  export default Card;

  //User.tsx
  import React from "react";
  import Card from "./Card";

  type UserProps = {
    user: {
      name: string;
      email: string;
      age: number;
      isRegistered: boolean;
      languages: string[];
    };
  };
  const User = ({ user }: UserProps) => {
    return (
      <Card>
        <h2>{user.name}</h2>
        <p>{user.email}</p>
        <p>{user.age} years old</p>
        {user.isRegistered ? (
          <p>Registered Student</p>
        ) : (
          <p>Unregistered Student</p>
        )}
        <p>
          Speaks:{" "}
          {user.languages.map((language, index) => {
            return <span key={index}>{language} </span>;
          })}
        </p>
      </Card>
    );
  };
  export default User;
  ```

## 5. Typing Event Props

- example
  ```tsx
      // Typing event props
    click event: event: React.MouseEvent<HTMLButtonElement>
    type ButtonProps = {
    handleClick: (event: React.MouseEvent<HTMLButtonElement>) => void;
    handleChange: (event: React.ChangeEvent<HTMLInputElement>) => void
    };
  ```

## 6. Style Props

- example

  ```tsx
  // props for styles -> React.CSSProperties
  import React from "react";

  type ButtonProps = {
    styles: React.CSSProperties;
  };

  const Button = (props: ButtonProps) => {
    return <button style={props.styles}>click me</button>;
  };

  export default Button;

  import "./App.css";
  import Button from "./components/Button";

  function App() {
    return (
      <div className="App">
        <Button
          styles={{ backgroundColor: "green", padding: "1rem", color: "white" }}
        />
      </div>
    );
  }

  export default App;
  ```

## 7. Typing useState Hooks

- example

  ```tsx
  import React, { useState } from "react";
  import "./App.css";

  const App = () => {
    // type is automatically infereed as number
    const [count, setCount] = useState(0);

    const handleIncrement = (): void => {
      setCount((count) => count + 1);
    };

    const handleDecrement = (): void => {
      setCount((count) => count - 1);
    };

    return (
      <div className="App">
        <h1>Count : {count}</h1>
        <button onClick={handleIncrement}>+</button>
        <button onClick={handleDecrement}>-</button>
      </div>
    );
  };

  export default App;

  // dealing with future values in useState Hook
  import React, { useState } from "react";
  import "./App.css";

  type User = {
    id: number;
    name: string;
  };

  const App = () => {
    // const [data, setData] = useState<null | string>(null);
    const [data, setData] = useState<null | User>(null);

    const handleSetData = () => {
      // setData("Anisul islam");
      setData({ id: 101, name: "anisul islam" });
      console.log(data);
    };

    return (
      <div className="App">
        <h1>UseState Future value</h1>
        <button onClick={handleSetData}>set data</button>
        {/* {data && <p>{data}</p>} */}
      <!-- <p>{data?.id}</p> -->
      <!-- <p>{data?.name}</p> -->
      </div>
    );
  };

  export default App;

  // type asertion - without optional chaining operator
  import React, { useState } from "react";
  import "./App.css";

  type User = {
    id: number;
    name: string;
  };

  const App = () => {
    // const [data, setData] = useState<null | string>(null);
    const [data, setData] = useState<User>({} as User);

    const handleSetData = () => {
      // setData("Anisul islam");
      setData({ id: 101, name: "anisul islam" });
      console.log(data);
    };

    return (
      <div className="App">
        <h1>UseState Future value</h1>
        <button onClick={handleSetData}>set data</button>
        {/* {data && <p>{data}</p>} */}
        <p>{data.id}</p>
        <p>{data.name}</p>
      </div>
    );
  };

  export default App;
  ```

## 8. Typing useReducer Hooks

- example

  ```tsx
  import React, { useReducer, useState } from "react";
  import "./App.css";

  type CounterState = {
    count: number;
  };

  type CounterAction = {
    type: string;
    payload?: number;
  };

  const initialState = {
    count: 0,
  };

  const reducer = (state: CounterState, action: CounterAction) => {
    switch (action.type) {
      case "INCREMENT":
        return {
          ...state,
          count: state.count + 1,
        };
      case "RESET":
        return {
          ...state,
          count: 0,
        };
      case "DECREMENT":
        return {
          ...state,
          count: state.count - 1,
        };

      default:
        return state;
    }
  };

  const App = () => {
    // const [count, setCount] = useState(0);
    const [state, dispatch] = useReducer(reducer, initialState);

    const handleIncrement = () => {
      dispatch({ type: "INCREMENT" });
    };

    const handleReset = () => {
      dispatch({ type: "RESET" });
    };

    const handleDecrement = () => {
      dispatch({ type: "DECREMENT" });
    };

    return (
      <div className="App">
        <h1>Count : {state.count}</h1>
        <button onClick={handleIncrement}>+</button>
        <button onClick={handleReset}>0</button>
        <button onClick={handleDecrement}>-</button>
      </div>
    );
  };

  export default App;

  //Restricting action types
  type CounterAction = {
    type: "INCREMENT" | "DECREMENT" | "RESET";
    payload?: number;
  };

  import React, { useReducer, useState } from "react";
  import "./App.css";

  type CounterState = {
    count: number;
  };

  type UpdateAction = {
    type: "INCREMENT" | "DECREMENT" | "RESET";
    payload?: number;
  };

  type CounterActionBy5 = {
    type: "INCREMENTBY5";
    payload: number;
  };

  const initialState = {
    count: 0,
  };

  type CounterAction = UpdateAction | CounterActionBy5;

  const reducer = (state: CounterState, action: CounterAction) => {
    switch (action.type) {
      case "INCREMENT":
        return {
          ...state,
          count: state.count + 1,
        };
      case "INCREMENTBY5":
        return {
          ...state,
          count: state.count + action.payload,
        };
      case "RESET":
        return {
          ...state,
          count: 0,
        };
      case "DECREMENT":
        return {
          ...state,
          count: state.count - 1,
        };

      default:
        return state;
    }
  };

  const App = () => {
    // const [count, setCount] = useState(0);
    const [state, dispatch] = useReducer(reducer, initialState);

    const handleIncrement = () => {
      dispatch({ type: "INCREMENT" });
    };
    const handleIncrementBy5 = () => {
      dispatch({ type: "INCREMENTBY5", payload: 5 });
    };

    const handleReset = () => {
      dispatch({ type: "RESET" });
    };

    const handleDecrement = () => {
      dispatch({ type: "DECREMENT" });
    };

    return (
      <div className="App">
        <h1>Count : {state.count}</h1>
        <button onClick={handleIncrement}>+</button>
        <button onClick={handleIncrementBy5}>+5</button>
        <button onClick={handleReset}>0</button>
        <button onClick={handleDecrement}>-</button>
      </div>
    );
  };

  export default App;
  ```
