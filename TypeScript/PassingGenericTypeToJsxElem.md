[Source](https://mariusschulz.com/blog/passing-generics-to-jsx-elements-in-typescript)

```javaScript
const SayHelloOrOtherThing: React.FC = ()=> {
    return <Message<String> message="hello">
}

function Message<T>({message}:IMessage<T>) {
    return <p>{message}</p>
}

interface IMessage<T> {
    message: T
}

```
