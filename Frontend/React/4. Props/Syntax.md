# Props Syntax

### Basic props

```tsx
const Greeting = (props) => {
  return <h1>Hello, {props.name}!</h1>;
};

const App = () => {
  return <Greeting name="Dude" />;
};
```

### Destructuring Props in Function Components
```tsx
const Greeting = ({ name }) => {
  return <h1>Hello, {name}!</h1>;
};

const App = () => {
  return <Greeting name="Dude" />;
};
```

### Default props
```tsx
const Greeting = ({ name = "Stranger" }) => {
  return <h1>Hello, {name}!</h1>;
};

const App = () => {
  return <Greeting />; // Will use default "Stranger"
};
```

### Props with Objects, Arrays
* Objects
```tsx
const UserCard = ({ user }) => {
  return <h2>{user.name} is {user.age} years old.</h2>;
};

const App = () => {
  const user = { name: "Dude", age: 25 };
  return <UserCard user={user} />;
};
```
* Arrays
```tsx
const List = ({ items }) => {
  return (
    <ul>
      {items.map((item, index) => (
        <li key={index}>{item}</li>
      ))}
    </ul>
  );
};

const App = () => {
  return <List items={["Apple", "Banana", "Cherry"]} />;
};
```

### Props with Functions (Callback Props)
```tsx
const Button = ({ onClick }) => {
  return <button onClick={onClick}>Click me</button>;
};

const App = () => {
  const handleClick = () => alert("Button clicked!");
  return <Button onClick={handleClick} />;
};
```

### Props with JSX Elements (Children Props)
```tsx
const Wrapper = ({ children }) => {
  return <div className="box">{children}</div>;
};

const App = () => {
  return (
    <Wrapper>
      <p>This is inside the wrapper!</p>
    </Wrapper>
  );
};
```

### Spread Operator for Props
```tsx
const Card = ({ title, content }) => {
  return (
    <div>
      <h2>{title}</h2>
      <p>{content}</p>
    </div>
  );
};

const App = () => {
  const cardProps = { title: "Hello", content: "This is a card." };
  return <Card {...cardProps} />;
};
```

### Prop Types with TypeScript
```tsx
type GreetingProps = {
  name: string;
  age?: number; // Optional prop
};

const Greeting: React.FC<GreetingProps> = ({ name, age }) => {
  return <h1>{name} {age && `is ${age} years old`}</h1>;
};

const App = () => <Greeting name="Dude" age={25} />;
```
You can define prop types inline using TypeScript like this:
```tsx
const Greeting = ({ name }: { name: string }) => {
  return <h1>Hello, {name}!</h1>;
};

const App = () => {
  return <Greeting name="Dude" />;
};
```
Or 
```tsx
type GreetingProps = {
  name: string;
  age?: number; // Optional prop
};

const Greeting = ({ name, age }: GreetingProps) => {
  return <h1>{name} {age && `is ${age} years old`}</h1>;
};

const App = () => <Greeting name="Dude" age={25} />;
```


