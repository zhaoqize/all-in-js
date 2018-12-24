## Refs 的三种写法

第一种：直接定义 `ref` 属性

```
class Button extends Component {
    constructor(props){
        super(props);
    }

    componentDidMount = () => {
        let btn = this.refs.btn;
        let link = this.refs.link;
    }
    
    render(){
        return (
            <div>
                <button ref='btn'>click</button>
                <a href='facebook.github.io/react' ref='link'>click</a>
            </div>
        )
    }
}
```

第二种：函数式写法

```
class Input extends Component {
    constructor(props){
        super(props);
    }
    
    focus = () => {
        this.textInput.focus();
    }
    
    render(){
        return (
            <div>
                <input ref={(input) => { this.textInput = input }} />
            </div>
        )
    }
}
```

第三种：使用 `React.createRef` 绑定

```
class MyComponent extends React.Component {
  constructor(props) {
    super(props);

    this.inputRef = React.createRef();
  }

  render() {
    return <input type="text" ref={this.inputRef} />;
  }

  componentDidMount() {
    this.inputRef.current.focus();
  }
}
```

## 参考&拓展：
- [从React官方文档看 refs 的使用和未来](https://juejin.im/post/5927f51244d904006414925a)
- [Refs & DOM](https://react.docschina.org/docs/refs-and-the-dom.html)