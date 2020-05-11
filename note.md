# React
## Reactプロジェクトの作り方
```sh
npx create-react-app my-app
```

## Reactとは
UIをコンポーネントに分割して組み上げるフレームワークの一つ。

## コンポーネント
propsと呼ばれるパラメータを受け取り、render メソッドを通じて、表示するビューの階層構造（React要素）を返す。この構造を書くのにJSX記法が用いられる。
```JS
return React.createElement('div', {className: 'shopping-list'},
  React.createElement('h1', /* ... h1 children ... */),
  React.createElement('ul', /* ... ul children ... */)
);
```
Vueと同じように、コンポーネント名をタグのように使用できる。また、プロパティに値を入れることで、値を渡すことができる。(このあたりの仕様はVueとほぼ同じ)
```JS
class Board extends React.Component {
  renderSquare(i) {
    return <Square value={i} />;
  }
}
```
this.propsに入れたプロパティが入っているので、取り出すのはVueよりも簡単。
```JS
class Square extends React.Component {
  render() {
    return (
      <button className="square">
        {this.props.value}
      </button>
    );
  }
}
```

## state
コンポーネントはコンストラクタでstateを指定することで、状態を持つことができる。

stateはsetStateメソッドにオブジェクトを渡すことで変更できる。

名前はstateだが、Vueのdataに相当する。
```JS
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }

  render() {
    return (
      <button
        className="square"
        onClick={() => this.setState({value: 'X'})}
      >
        {this.state.value}
      </button>
    );
  }
}
```

## 関数コンポーネント
render メソッドだけを有して自分の state を持たないコンポーネントを、よりシンプルに書くための方法。
```JS
function Square(props) {
  return (
    <button className="square" onClick={props.onClick}>
      {props.value}
    </button>
  );
}
```

## イミュータブル
sliceメソッドで配列のコピーを作って編集したり、pushではなく、concatを使って新しい配列を作ったりすることで直接の変更を避ける(イミュ―タビリティ；不変性)。

履歴の保持などの複雑な機能の実装や変更の検出の上でメリットがある。