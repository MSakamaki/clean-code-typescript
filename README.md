# clean-code-typescript [![Tweet](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/intent/tweet?text=Clean%20Code%20Typescript&url=https://github.com/labs42io/clean-code-typescript)

Clean Code concepts adapted for TypeScript.  
TypeScriptの為のクリーンコード

Inspired from [clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript).
[clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript)を見て閃きました。


## Table of Contents

  1. [Introduction](#introduction)
  2. [Variables](#variables)
  3. [Functions](#functions)
  4. [Objects and Data Structures](#objects-and-data-structures)
  5. [Classes](#classes)
  6. [SOLID](#solid)
  7. [Testing](#testing)
  8. [Concurrency](#concurrency)
  9. [Error Handling](#error-handling)
  10. [Formatting](#formatting)
  11. [Comments](#comments)

## Introduction

![Humorous image of software quality estimation as a count of how many expletives
you shout when reading code](https://www.osnews.com/images/comics/wtfm.jpg)

Software engineering principles, from Robert C. Martin's book
[*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882),
adapted for TypeScript. This is not a style guide. It's a guide to producing
[readable, reusable, and refactorable](https://github.com/ryanmcdermott/3rs-of-software-architecture) software in TypeScript.

Robert C. Martinの書籍 [*Clean Code*](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)をTypeScriptに対応させたソフトウェア工学の原則です。 [翻訳書籍(amazonへのリンク)](https://www.amazon.co.jp/dp/B078HYWY5X)
これはスタイルガイドではありません。
TypeScriptで可読性が高く、再利用可能であり、リファクタブルなソフトウェアを生産するためのガイドラインです。

Not every principle herein has to be strictly followed, and even fewer will be
universally agreed upon. These are guidelines and nothing more, but they are
ones codified over many years of collective experience by the authors of
*Clean Code*.

すべての原則に厳密に従う必要はありません、さらに一般に合意されているものはさらに少くなります。
これらはガイドライン以上でしかありませんが、*Clean Code* の著者達による長年の経験を集めて文書化したものです。

Our craft of software engineering is just a bit over 50 years old, and we are
still learning a lot. When software architecture is as old as architecture
itself, maybe then we will have harder rules to follow. For now, let these
guidelines serve as a touchstone by which to assess the quality of the
TypeScript code that you and your team produce.

ソフトウェア工学の歴史はほんの50年を少し超えた程度であり、未だに私達は多くのことを学び続けています。
ソフトウェアアーキテクチャが建築と同くらい歴史を持っていたならば、おそらく従うべき原則はより厳しくなっていたでしょう。
現時点では、このガイドラインは、あなたとあなたのチームが作成したTypeScriptコードの品質を評価するための基準として役立つでしょう。

One more thing: knowing these won't immediately make you a better software
developer, and working with them for many years doesn't mean you won't make
mistakes. Every piece of code starts as a first draft, like wet clay getting
shaped into its final form. Finally, we chisel away the imperfections when
we review it with our peers. Don't beat yourself up for first drafts that need
improvement. Beat up the code instead!

それからもう一つ：
これらを知ったからと言ってすぐに優秀なソフトウェア開発者となるわけではありませんし、長年これに従って作業を行っても間違いを犯さないわけではありません。
湿った粘土が最終的な形になるように、コードの各部分は最初のドラフト（ルール）になります。
最終的に同僚とこれをレビューする時、不完全な部分を取り除いていきます。
最初のドラフトに改善が必要となった時、自分自身を責めないでください。
代わりにコードを責めましょう！


**[⬆ back to top](#table-of-contents)**

## Variables

## 変数

### Use meaningful variable names 

### 意味のある変数名を使う

Distinguish names in such a way that the reader knows what the differences offer.

何を意味してるかを読み手が区別できる名前を付けましょう。

**Bad:**

```ts
function between<T>(a1: T, a2: T, a3: T): boolean {
  return a2 <= a1 && a1 <= a3;
}

```

**Good:**

```ts
function between<T>(value: T, left: T, right: T): boolean {
  return left <= value && value <= right;
}
```

**[⬆ back to top](#table-of-contents)**

### Use pronounceable variable names

### 発音可能な変数名を使う

If you can’t pronounce it, you can’t discuss it without sounding like an idiot.

あなたがそれを発音できないなら、まぬけに聞こえてまともな論議になりません。

**Bad:**

```ts
type DtaRcrd102 = {
  genymdhms: Date;
  modymdhms: Date;
  pszqint: number;
}
```

**Good:**

```ts
type Customer = {
  generationTimestamp: Date;
  modificationTimestamp: Date;
  recordId: number;
}
```

**[⬆ back to top](#table-of-contents)**

### Use the same vocabulary for the same type of variable

### 同じ型の変数には同じ単語を割り当てる。

**Bad:**

```ts
function getUserInfo(): User;
function getUserDetails(): User;
function getUserData(): User;
```

**Good:**

```ts
function getUser(): User;
```

**[⬆ back to top](#table-of-contents)**

### Use searchable names

### 検索可能な名前を使う

We will read more code than we will ever write. It's important that the code we do write is readable and searchable. By not naming variables that end up being meaningful for understanding our program, we hurt our readers. Make your names searchable. Tools like [TSLint](https://palantir.github.io/tslint/rules/no-magic-numbers/) can help identify unnamed constants.

私達は書いた以上のコードを読むでしょう。
そのため書いたコードは読みやすく探しやすいコードであることが重要になってきます。
プログラムを理解するのに重要な意味がある変数に名前を付けないことによって、私達は読み手を傷つけています。
名前を付ける時は検索しやすいものにしましょう。
[TSLint](https://palantir.github.io/tslint/rules/no-magic-numbers/)のようなツールは、名前のない定数を識別するのに役立ちます。

**Bad:**

```ts
// What the heck is 86400000 for?
// 一体何が86400000なのか？
setTimeout(restart, 86400000);
```

**Good:**

```ts
// Declare them as capitalized named constants.
// 定数の名前は大文字で宣言してください。
const MILLISECONDS_IN_A_DAY = 24 * 60 * 60 * 1000;

setTimeout(restart, MILLISECONDS_IN_A_DAY);
```

**[⬆ back to top](#table-of-contents)**

### Use explanatory variables

### 説明変数を使う

**Bad:**

```ts
declare const users: Map<string, User>;

for (const keyValue of users) {
  // iterate through users map
  // user map を反復処理する
}
```

**Good:**

```ts
declare const users: Map<string, User>;

for (const [id, user] of users) {
  // iterate through users map
  // user map を反復処理する
}
```

**[⬆ back to top](#table-of-contents)**

### Avoid Mental Mapping

### メンタルマップを避ける

Explicit is better than implicit.
*Clarity is king.*

明示的は暗黙的より優れています。
*Clarity is king.*

**Bad:**

```ts
const u = getUser();
const s = getSubscription();
const t = charge(u, s);
```

**Good:**

```ts
const user = getUser();
const subscription = getSubscription();
const transaction = charge(user, subscription);
```

**[⬆ back to top](#table-of-contents)**

### Don't add unneeded context

### 不要な文脈を追加しない

If your class/type/object name tells you something, don't repeat that in your variable name.

もしあなたの class/type/object の名前が何かを伝えているのなら、あなたの変数名の中でそのことを繰り返さないでください。

**Bad:**

```ts
type Car = {
  carMake: string;
  carModel: string;
  carColor: string;
}

function print(car: Car): void {
  console.log(`${car.carMake} ${car.carModel} (${car.carColor})`);
}
```

**Good:**

```ts
type Car = {
  make: string;
  model: string;
  color: string;
}

function print(car: Car): void {
  console.log(`${car.make} ${car.model} (${car.color})`);
}
```

**[⬆ back to top](#table-of-contents)**

### Use default arguments instead of short circuiting or conditionals

### 短絡評価や条件式の代わりにデフォルト引数を使用する

Default arguments are often cleaner than short circuiting.

デフォルト引数は、短絡評価よりもきれいなことがよくあります。

**Bad:**

```ts
function loadPages(count?: number) {
  const loadCount = count !== undefined ? count : 10;
  // ...
}
```

**Good:**

```ts
function loadPages(count: number = 10) {
  // ...
}
```

**[⬆ back to top](#table-of-contents)**

## Functions

## 関数

### Function arguments (2 or fewer ideally)

### 関数の引数 (理想は２つ以下)

Limiting the amount of function parameters is incredibly important because it makes testing your function easier.
Having more than three leads to a combinatorial explosion where you have to test tons of different cases with each separate argument.  

関数における引数の数を制限することは非常に重要です。
なぜならそれは貴方の関数のテストをシンプルにするからです。
3つ以上になると、引数ごとの数だけ違うケースをテストしなければならず、組み合わせは爆発的に増加します。

One or two arguments is the ideal case, and three should be avoided if possible. Anything more than that should be consolidated.
Usually, if you have more than two arguments then your function is trying to do too much.
In cases where it's not, most of the time a higher-level object will suffice as an argument.  

理想的な引数の数は１〜２個であり、３つは避けるべきであり。
それ以上の数になるならば結合するべきです。
普通は2つ以上の引数がある場合、関数がやりすぎています。
そうでない場合は、上位のオブジェクトを引数にすれば十分です。

Consider using object literals if you are finding yourself needing a lot of arguments.  

たくさんの引数が必要な場合はオブジェクトリテラルの利用を検討してください。

To make it obvious what properties the function expects, you can use the [destructuring](https://basarat.gitbooks.io/typescript/docs/destructuring.html) syntax.

関数がどのようなプロパティを持っているかを明示的にするた めに、[destructuring](https://basarat.gitbooks.io/typescript/docs/destructuring.html)構文を使うことができます。

This has a few advantages:

1. When someone looks at the function signature, it's immediately clear what properties are being used.

2. Destructuring also clones the specified primitive values of the argument object passed into the function. This can help prevent side effects. Note: objects and arrays that are destructured from the argument object are NOT cloned.

3. TypeScript warns you about unused properties, which would be impossible without destructuring.

これにはいくつかの利点があります:

1. 誰かが関数の入出力を見た時に、どのプロパティが利用されているのかがすぐにわかります。

2. 分割代入は、関数に渡された引数オブジェクトのプリミティブ型の値を複製します。これは副作用を防ぐのに役立ちます
   注釈：引数オブジェクトから分割代入されたObjectとArrayは複製されません。

3. TypeScriptは未使用のプロパティについて警告します、これは分割代入なしでは不可能でしょう。

**Bad:**

```ts
function createMenu(title: string, body: string, buttonText: string, cancellable: boolean) {
  // ...
}

createMenu('Foo', 'Bar', 'Baz', true);
```

**Good:**

```ts
function createMenu(options: { title: string, body: string, buttonText: string, cancellable: boolean }) {
  // ...
}

createMenu({
  title: 'Foo',
  body: 'Bar',
  buttonText: 'Baz',
  cancellable: true
});
```

You can further improve readability by using [type aliases](https://www.typescriptlang.org/docs/handbook/advanced-types.html#type-aliases):

[タイプエイリアス](https://www.typescriptlang.org/docs/handbook/advanced-types.html#type-aliases)を使うことで、さらに読みやすさ向上させることができます。

```ts

type MenuOptions = { title: string, body: string, buttonText: string, cancellable: boolean };

function createMenu(options: MenuOptions) {
  // ...
}

createMenu({
  title: 'Foo',
  body: 'Bar',
  buttonText: 'Baz',
  cancellable: true
});
```

**[⬆ back to top](#table-of-contents)**

### Functions should do one thing

### 関数は１つのことだけを行うべきです

This is by far the most important rule in software engineering. When functions do more than one thing, they are harder to compose, test, and reason about. When you can isolate a function to just one action, they can be refactored easily and your code will read much cleaner. If you take nothing else away from this guide other than this, you'll be ahead of many developers.

これはソフトウェア・エンジニアリングにおいて、とても重要なルールです。
関数が1つ以上のことをするとき、それは作成してテストし、推測することをより困難にします。
関数を一つの振る舞いに分離することができれば、それらは簡単にリファクタリングすることができるようになり、あなたのコードはとても綺麗になります。
このガイドのこの項以外を何もしなかったとしても、あなたは他の多くの開発者よりも一歩先を行ってるでしょう。

**Bad:**

```ts
function emailClients(clients: Client) {
  clients.forEach((client) => {
    const clientRecord = database.lookup(client);
    if (clientRecord.isActive()) {
      email(client);
    }
  });
}
```

**Good:**

```ts
function emailClients(clients: Client) {
  clients.filter(isActiveClient).forEach(email);
}

function isActiveClient(client: Client) {
  const clientRecord = database.lookup(client);
  return clientRecord.isActive();
}
```

**[⬆ back to top](#table-of-contents)**

### Function names should say what they do

### 関数名は何をするべきか宣言するべきです。

**Bad:**

```ts
function addToDate(date: Date, month: number): Date {
  // ...
}

const date = new Date();

// It's hard to tell from the function name what is added
// 何が追加されたかを、関数名から予測することができません。
addToDate(date, 1);
```

**Good:**

```ts
function addMonthToDate(date: Date, month: number): Date {
  // ...
}

const date = new Date();
addMonthToDate(date, 1);
```

**[⬆ back to top](#table-of-contents)**

### Functions should only be one level of abstraction

### 関数は一つの抽象化に留めること。

When you have more than one level of abstraction your function is usually doing too much. Splitting up functions leads to reusability and easier testing.

あなたが１つ以上の抽象化を行っている時、関数はやりすぎています。
機能を分割すれば再利用性とテスト用意性を向上させることができます。

**Bad:**

```ts
function parseCode(code: string) {
  const REGEXES = [ /* ... */ ];
  const statements = code.split(' ');
  const tokens = [];

  REGEXES.forEach((regex) => {
    statements.forEach((statement) => {
      // ...
    });
  });

  const ast = [];
  tokens.forEach((token) => {
    // lex...
  });

  ast.forEach((node) => {
    // parse...
  });
}
```

**Good:**

```ts
const REGEXES = [ /* ... */ ];

function parseCode(code: string) {
  const tokens = tokenize(code);
  const syntaxTree = parse(tokens);

  syntaxTree.forEach((node) => {
    // parse...
  });
}

function tokenize(code: string): Token[] {
  const statements = code.split(' ');
  const tokens: Token[] = [];

  REGEXES.forEach((regex) => {
    statements.forEach((statement) => {
      tokens.push( /* ... */ );
    });
  });

  return tokens;
}

function parse(tokens: Token[]): SyntaxTree {
  const syntaxTree: SyntaxTree[] = [];
  tokens.forEach((token) => {
    syntaxTree.push( /* ... */ );
  });

  return syntaxTree;
}
```

**[⬆ back to top](#table-of-contents)**

### Remove duplicate code

### 承服したコードは消す

Do your absolute best to avoid duplicate code.
Duplicate code is bad because it means that there's more than one place to alter something if you need to change some logic.  

コードの重複を避ける事に最善を尽くしてください。
重複したコードがあるということは、ロジックの変更を行う時に複数の箇所に同じ変更をする必要があるため、よくありません。

Imagine if you run a restaurant and you keep track of your inventory: all your tomatoes, onions, garlic, spices, etc.
If you have multiple lists that you keep this on, then all have to be updated when you serve a dish with tomatoes in them.
If you only have one list, there's only one place to update!  

貴方がレストランを経営していたとしましょう、そして在庫整理しているとします: トマト、玉ねぎ、ニンニク、スパイスなど、すべてあなたの物です。
貴方がこの在庫を管理するリストを複数持っていた場合、トマト料理を提供したらリストすべてを更新する必要がでてきます。
リストが１つだけなら、更新は１箇所済むでしょう！

Oftentimes you have duplicate code because you have two or more slightly different things, that share a lot in common, but their differences force you to have two or more separate functions that do much of the same things. Removing duplicate code means creating an abstraction that can handle this set of different things with just one function/module/class.  

共通点が多いが、２つ以上の小さな違いがあるために、コードが重複してしまうことはよくあります。
しかしその結果、その違いによってほとんど同じことを行う２つ以上の関数が必要になってしまいます。
重複したコードを削除するということは、一つの関数/モジュール/クラスで、これらの僅かに異なる一連のものを処理できる抽象化を作るということを意味します。

Getting the abstraction right is critical, that's why you should follow the [SOLID](#solid) principles. Bad abstractions can be worse than duplicate code, so be careful! Having said this, if you can make a good abstraction, do it! Don't repeat yourself, otherwise you'll find yourself updating multiple places anytime you want to change one thing.

抽象化を正しく行うことが重要です。
そのため、SOLID の原則に従う必要があります。
悪い抽象化はコードの重複よりも悪い場合があるので注意してください!
とは言うものの、あなたが良い抽象化をすることができるのであれば、是非行うべきです！
同じことをしないでください、そうしなければ何か一つを変更したい時、複数の場所を変更することになってしまいます。

**Bad:**

```ts
function showDeveloperList(developers: Developer[]) {
  developers.forEach((developer) => {
    const expectedSalary = developer.calculateExpectedSalary();
    const experience = developer.getExperience();
    const githubLink = developer.getGithubLink();

    const data = {
      expectedSalary,
      experience,
      githubLink
    };

    render(data);
  });
}

function showManagerList(managers: Manager[]) {
  managers.forEach((manager) => {
    const expectedSalary = manager.calculateExpectedSalary();
    const experience = manager.getExperience();
    const portfolio = manager.getMBAProjects();

    const data = {
      expectedSalary,
      experience,
      portfolio
    };

    render(data);
  });
}
```

**Good:**

```ts
class Developer {
  // ...
  getExtraDetails() {
    return {
      githubLink: this.githubLink,
    }
  }
}

class Manager {
  // ...
  getExtraDetails() {
    return {
      portfolio: this.portfolio,
    }
  }
}

function showEmployeeList(employee: Developer | Manager) {
  employee.forEach((employee) => {
    const expectedSalary = employee.calculateExpectedSalary();
    const experience = employee.getExperience();
    const extra = employee.getExtraDetails();

    const data = {
      expectedSalary,
      experience,
      extra,
    };

    render(data);
  });
}
```

You should be critical about code duplication. Sometimes there is a tradeoff between duplicated code and increased complexity by introducing unnecessary abstraction. When two implementations from two different modules look similar but live in different domains, duplication might be acceptable and preferred over extracting the common code. The extracted common code in this case introduces an indirect dependency between the two modules.

あなたはコードの重複について批判的であるべきです。
不必要な抽象化を導入することによって、コードの重複と複雑さの増大との間にトレードオフがあることがあります。
２つの異なるモジュールから呼ばれている２つの実装が似ているように見えても、異なるドメインに存在する場合は重複が許容され、共通コードの抽出よりも優先される場合があります。
この時に抽出された共通コードは、２つのモジュールの間に間接的な依存関係をもたらします。

**[⬆ back to top](#table-of-contents)**

### Set default objects with Object.assign or destructuring

**Bad:**

```ts
type MenuConfig = { title?: string, body?: string, buttonText?: string, cancellable?: boolean };

function createMenu(config: MenuConfig) {
  config.title = config.title || 'Foo';
  config.body = config.body || 'Bar';
  config.buttonText = config.buttonText || 'Baz';
  config.cancellable = config.cancellable !== undefined ? config.cancellable : true;

  // ...
}

createMenu({ body: 'Bar' });
```

**Good:**

```ts
type MenuConfig = { title?: string, body?: string, buttonText?: string, cancellable?: boolean };

function createMenu(config: MenuConfig) {
  const menuConfig = Object.assign({
    title: 'Foo',
    body: 'Bar',
    buttonText: 'Baz',
    cancellable: true
  }, config);

  // ...
}

createMenu({ body: 'Bar' });
```

Alternatively, you can use destructuring with default values:

デフォルト値を利用した分割代入を使う手もあるでしょう：

```ts
type MenuConfig = { title?: string, body?: string, buttonText?: string, cancellable?: boolean };

function createMenu({ title = 'Foo', body = 'Bar', buttonText = 'Baz', cancellable = true }: MenuConfig) {
  // ...
}

createMenu({ body: 'Bar' });
```

To avoid any side effects and unexpected behavior by passing in explicitly the `undefined` or `null` value, you can tell the TypeScript compiler to not allow it.
See [`--strictNullChecks`](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html#--strictnullchecks) option in TypeScript.

明示的に `undefined` や `null` の値を渡して副作用や予期しない動作を避けるため、TypeScriptコンパイラにそれを許容させない設定もできます。
TypeScriptの [`--strictNullChecks`](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-2-0.html#--strictnullchecks) 設定を参照

**[⬆ back to top](#table-of-contents)**

### Don't use flags as function parameters

### 関数の引数にフラグは渡さない

Flags tell your user that this function does more than one thing.
Functions should do one thing. Split out your functions if they are following different code paths based on a boolean.

フラグは、この関数が複数の事をしていと利用者に伝えています。
関数は一つのことをするべきなので、Boolean値によって異なる処理をしている場合は関数を別にします。

**Bad:**

```ts
function createFile(name: string, temp: boolean) {
  if (temp) {
    fs.create(`./temp/${name}`);
  } else {
    fs.create(name);
  }
}
```

**Good:**

```ts
function createTempFile(name: string) {
  createFile(`./temp/${name}`);
}

function createFile(name: string) {
  fs.create(name);
}
```

**[⬆ back to top](#table-of-contents)**

### Avoid Side Effects (part 1)

### 副作用を避ける（その１）

A function produces a side effect if it does anything other than take a value in and return another value or values.
A side effect could be writing to a file, modifying some global variable, or accidentally wiring all your money to a stranger.  

関数が値を受け取り何かを返す以外の事をした場合、副作用を引き起こします。
副作用とはファイルへの書き込みや、グローバル変数の変更、間違って全財産を見知らぬ他人に振り込んでしまうような事です。

Now, you do need to have side effects in a program on occasion. Like the previous example, you might need to write to a file.
What you want to do is to centralize where you are doing this. Don't have several functions and classes that write to a particular file.
Have one service that does it. One and only one.  

前に上げた例のように、ファイルに書き込む必要があるかもしれません。
やるべきことは、それを行う場所を一つの場所に留めることです。
特定のファイルに書き込む関数やクラスが複数存在しないようにしてください。
それをする、唯一無二のサービスを作ります。

The main point is to avoid common pitfalls like sharing state between objects without any structure, using mutable data types that can be written to by anything, and not centralizing where your side effects occur. If you can do this, you will be happier than the vast majority of other programmers.
重要なのは、構造を持たずオブジェクト間で状態を共有したり、任意のものに書き込み可能な可変データ型を使ったり、副作用が発生する場所を一箇所にしないなどの、一般的な落とし穴を避けることです。
貴方がこれをできるようになれば、大多数の他のプログラマーより幸せになれるでしょう。


**Bad:**

```ts
// Global variable referenced by following function.
// 以下の関数で利用されるグローバル変数
let name = 'Robert C. Martin';

function toBase64() {
  name = btoa(name);
}

toBase64();
// If we had another function that used this name, now it'd be a Base64 value
// 変数 name を使用した別の関数がある場合は、その中身はBase64になります。

console.log(name); // expected to print 'Robert C. Martin' but instead 'Um9iZXJ0IEMuIE1hcnRpbg=='
                   // 'Robert C. Martin' と表示されるはずが、'Um9iZXJ0IEMuIE1hcnRpbg=='と表示されてしまう
```

**Good:**

```ts
const name = 'Robert C. Martin';

function toBase64(text: string): string {
  return btoa(text);
}

const encodedName = toBase64(name);
console.log(name);
```

**[⬆ back to top](#table-of-contents)**

### Avoid Side Effects (part 2)

### 副作用を避ける(その２)

In JavaScript, primitives are passed by value and objects/arrays are passed by reference. In the case of objects and arrays, if your function makes a change in a shopping cart array, for example, by adding an item to purchase, then any other function that uses that cart array will be affected by this addition. That may be great, however it can be bad too. Let's imagine a bad situation:  

JavaScriptではプリミティブ型は値で渡され、オブジェクトや配列は参照によって渡されます。
オブジェクトや配列の場合、商品を購入するなどしてショッピングカート配列を更新した場合、ショッピングカート配列を使用する他のすべての関数が追加の影響を受けてしまいます。
それは素晴らしく思えますが、悪いことも起こります。
悪い状況を想像してみましょう。

The user clicks the "Purchase", button which calls a purchase function that spawns a network request and sends the cart array to the server. Because of a bad network connection, the purchase function has to keep retrying the request. Now, what if in the meantime the user accidentally clicks "Add to Cart" button on an item they don't actually want before the network request begins? If that happens and the network request begins, then that purchase function will send the accidentally added item because it has a reference to a shopping cart array that the *addItemToCart* function modified by adding an unwanted item.  

ユーザーが"購入"ボタンをクリックすると、ネットワークのリクエストを生成してカート配列をサーバーに送信する、*purchase*  関数が呼ばれます。
ネットワークの状況が悪いため、*purchase* 関数は要求を繰り返し続けなければいけません。
そして、ネットワークのリクエストが成功する前にユーザーがほしくないアイテムを"カートに入れる"ボタンを誤って押してしまったらどうなるでしょうか？
ネットワークのリクエストが成功した時 *addItemToCart* 関数はカート配列への参照を持っていたため、 不要なアイテムをカート配列へ追加してしまいます、*purchase* 関数は間違って追加された商品を送信してしまいます。

A great solution would be for the *addItemToCart* to always clone the cart, edit it, and return the clone. This ensures that no other functions that are holding onto a reference of the shopping cart will be affected by any changes.  

良い解決策は  *addItemToCart* 関数が常にカートのクローンを作成し、それを編集してさらにクローンを返すことです。
これで、ショッピングカート配列の参照を保持している他の関数が変更の影響を受けなくなります。

Two caveats to mention to this approach:

1. There might be cases where you actually want to modify the input object, but when you adopt this programming practice you will find that those cases are pretty rare. Most things can be refactored to have no side effects! (see [pure function](https://en.wikipedia.org/wiki/Pure_function))

2. Cloning big objects can be very expensive in terms of performance. Luckily, this isn't a big issue in practice because there are great libraries that allow this kind of programming approach to be fast and not as memory intensive as it would be for you to manually clone objects and arrays.

このアプローチにおける２つの注意点：

1. 時には渡されたオブジェクト型を変更したい場合があるケースがありますが、このプログラミング手法を採用している場合にそういったケースは稀ということに気づくでしょう。
そして殆どの場合、副作用がないようなリファクタリングを行うことが可能です。
 ([純粋関数](https://en.wikipedia.org/wiki/Pure_function)を参照)

2. 大きなオブジェクトの複製を作成すると、パフォーマンスの面で非常に高コストになってしまう可能性があります。幸運なことに、これは実際には大きな問題ではありません。
なぜなら、手動でオブジェクトや配列を複製するのとは異なり、この種のプログラミング手法をより高速でメモリ使用量を抑えた素晴らしいライブラリがあるからです。

**Bad:**

```ts
function addItemToCart(cart: CartItem[], item: Item): void {
  cart.push({ item, date: Date.now() });
};
```

**Good:**

```ts
function addItemToCart(cart: CartItem[], item: Item): CartItem[] {
  return [...cart, { item, date: Date.now() }];
};
```

**[⬆ back to top](#table-of-contents)**

### Don't write to global functions

### グローバル関数には書き込まなh

Polluting globals is a bad practice in JavaScript because you could clash with another library and the user of your API would be none-the-wiser until they get an exception in production. Let's think about an example: what if you wanted to extend JavaScript's native Array method to have a diff method that could show the difference between two arrays? You could write your new function to the `Array.prototype`, but it could clash with another library that tried to do the same thing. What if that other library was just using `diff` to find the difference between the first and last elements of an array? This is why it would be much better to just use classes and simply extend the `Array` global.

グローバルを汚染するのはJavaScriptのバッドプラクティスです。
なぜなら他のライブラリをクラッシュさせるかもしれないし、あなたのAPIを使ってるユーザーは本番環境で例外が発生するまで何が起こってるか分からないからです。
例を考えてみましょう。
２つの配列の違いを差分を出すdiffメソッドを、既存JavaScriptのArrayに追加したらどうなりますか？
新しい関数を `Array.prototype` に書くことはできますが、同じことをしている他のライブラリと衝突する可能性があります。
他のライブラリが単に配列の最初の要素と最後の要素の違いを見つけるために `diff` を使っていたとしたらどうなるでしょうか。
これが、グローバルの`Array`を拡張するより `class` を使ったほうが良い理由です。

**Bad:**

```ts
declare global {
  interface Array<T> {
    diff(other: T[]): Array<T>;
  }
}

if (!Array.prototype.diff) {
  Array.prototype.diff = function <T>(other: T[]): T[] {
    const hash = new Set(other);
    return this.filter(elem => !hash.has(elem));
  };
}
```

**Good:**

```ts
class MyArray<T> extends Array<T> {
  diff(other: T[]): T[] {
    const hash = new Set(other);
    return this.filter(elem => !hash.has(elem));
  };
}
```

**[⬆ back to top](#table-of-contents)**

### Favor functional programming over imperative programming

### 命令形プログラミングより関数型プログラミングを好む

Favor this style of programming when you can.

できるなら、あなたはこのプログラミングスタイルを好きになってください。

**Bad:**

```ts
const contributions = [
  {
    name: 'Uncle Bobby',
    linesOfCode: 500
  }, {
    name: 'Suzie Q',
    linesOfCode: 1500
  }, {
    name: 'Jimmy Gosling',
    linesOfCode: 150
  }, {
    name: 'Gracie Hopper',
    linesOfCode: 1000
  }
];

let totalOutput = 0;

for (let i = 0; i < contributions.length; i++) {
  totalOutput += contributions[i].linesOfCode;
}
```

**Good:**

```ts
const contributions = [
  {
    name: 'Uncle Bobby',
    linesOfCode: 500
  }, {
    name: 'Suzie Q',
    linesOfCode: 1500
  }, {
    name: 'Jimmy Gosling',
    linesOfCode: 150
  }, {
    name: 'Gracie Hopper',
    linesOfCode: 1000
  }
];

const totalOutput = contributions
  .reduce((totalLines, output) => totalLines + output.linesOfCode, 0);
```

**[⬆ back to top](#table-of-contents)**

### Encapsulate conditionals

### 条件をカプセル化する。

**Bad:**

```ts
if (subscription.isTrial || account.balance > 0) {
  // ...
}
```

**Good:**

```ts
function canActivateService(subscription: Subscription, account: Account) {
  return subscription.isTrial || account.balance > 0
}

if (canActivateService(subscription, account)) {
  // ...
}
```

**[⬆ back to top](#table-of-contents)**

### Avoid negative conditionals

### 否定的な条件を避ける

**Bad:**

```ts
function isEmailNotUsed(email: string): boolean {
  // ...
}

if (isEmailNotUsed(email)) {
  // ...
}
```

**Good:**

```ts
function isEmailUsed(email): boolean {
  // ...
}

if (!isEmailUsed(node)) {
  // ...
}
```

**[⬆ back to top](#table-of-contents)**

### Avoid conditionals

### 条件を避ける

This seems like an impossible task. Upon first hearing this, most people say, "how am I supposed to do anything without an `if` statement?" The answer is that you can use polymorphism to achieve the same task in many cases. The second question is usually, "well that's great but why would I want to do that?" The answer is a previous clean code concept we learned: a function should only do one thing. When you have classes and functions that have `if` statements, you are telling your user that your function does more than one thing. Remember, just do one thing.

これは一見不可能な作業に見えます。
これを聞いた時、ほとんどの人は「if文を使わないとしたらどうすれば良いのか？」と言います。
この答えは、多くの場合、同じタスクをするためにポリモーフィズム(多態性・多様性)を利用するということです。
２つめの質問としてよくあるのは「素晴らしいことだと思うが、なんでそれをする必要があるのか？」といったものです。
この答えは、私達が先に学んだクリーンコードの概念「関数はただ一つのことをするべき」だからです。
貴方のクラスや関数がif文を持っている時、この関数は複数のことを示しています。
関数は唯一つのことをやるということを覚えておいてください。

**Bad:**

```ts
class Airplane {
  private type: string;
  // ...

  getCruisingAltitude() {
    switch (this.type) {
      case '777':
        return this.getMaxAltitude() - this.getPassengerCount();
      case 'Air Force One':
        return this.getMaxAltitude();
      case 'Cessna':
        return this.getMaxAltitude() - this.getFuelExpenditure();
      default:
        throw new Error('Unknown airplane type.');
    }
  }

  private getMaxAltitude(): number {
    // ...
  }
}
```

**Good:**

```ts
abstract class Airplane {
  protected getMaxAltitude(): number {
    // shared logic with subclasses ...
  }

  // ...
}

class Boeing777 extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude() - this.getPassengerCount();
  }
}

class AirForceOne extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude();
  }
}

class Cessna extends Airplane {
  // ...
  getCruisingAltitude() {
    return this.getMaxAltitude() - this.getFuelExpenditure();
  }
}
```

**[⬆ back to top](#table-of-contents)**

### Avoid type checking

### 型チェックを避ける

TypeScript is a strict syntactical superset of JavaScript and adds optional static type checking to the language.
Always prefer to specify types of variables, parameters and return values to leverage the full power of TypeScript features.
It makes refactoring more easier.

TypeScriptはJavaScriptの厳密な構文スーパセットであり、言語へ静的型チェックのオプションを追加します。
TypeScriptの機能を最大限に活用するには、常に変数、パラメータ、戻り値の方を指定する事をおすすめします。
これはリファクタリングをより簡単にします。

**Bad:**

```ts
function travelToTexas(vehicle: Bicycle | Car) {
  if (vehicle instanceof Bicycle) {
    vehicle.pedal(currentLocation, new Location('texas'));
  } else if (vehicle instanceof Car) {
    vehicle.drive(currentLocation, new Location('texas'));
  }
}
```

**Good:**

```ts
type Vehicle = Bicycle | Car;

function travelToTexas(vehicle: Vehicle) {
  vehicle.move(currentLocation, new Location('texas'));
}
```

**[⬆ back to top](#table-of-contents)**

### Don't over-optimize

### 行き過ぎた最適化を避ける

Modern browsers do a lot of optimization under-the-hood at runtime. A lot of times, if you are optimizing then you are just wasting your time. There are good [resources](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers) for seeing where optimization is lacking. Target those in the meantime, until they are fixed if they can be.

今のブラウザは実行時に内部で多くの最適化を行っています。
貴方が最適化に多数の時間を費やしてるなら、あなたは時間を無駄にしています。
最適化ができていないところを見るための良い[資料](https://github.com/petkaantonov/bluebird/wiki/Optimization-killers)があります。
それらが最適化されるまでは、そこだけを最適化の対象にしてください。

**Bad:**

```ts
// On old browsers, each iteration with uncached `list.length` would be costly
// because of `list.length` recomputation. In modern browsers, this is optimized.
// 古いブラウザは、キャッシュされていない `list.length` を使った繰り返しはコストがかかるでしょう
// なぜなら、呼ばれるたびに  `list.length`  が再計算されるから。 モダンブラウザは最適化されている
for (let i = 0, len = list.length; i < len; i++) {
  // ...
}
```

**Good:**

```ts
for (let i = 0; i < list.length; i++) {
  // ...
}
```

**[⬆ back to top](#table-of-contents)**

### 使っていないコードは削除する

Dead code is just as bad as duplicate code. There's no reason to keep it in your codebase.
If it's not being called, get rid of it! It will still be safe in your version history if you still need it.

使われていないコードは重複したコードと同じくらい悪いものです。
あなたのコードにそれを残しておく理由はありません。
もし参照がないなら取り除きましょう！必要と感じていたとしてもバージョン管理ツールの履歴に残っているだけで十分でしょう。

**Bad:**

```ts
function oldRequestModule(url: string) {
  // ...
}

function requestModule(url: string) {
  // ...
}

const req = requestModule;
inventoryTracker('apples', req, 'www.inventory-awesome.io');
```

**Good:**

```ts
function requestModule(url: string) {
  // ...
}

const req = requestModule;
inventoryTracker('apples', req, 'www.inventory-awesome.io');
```

**[⬆ back to top](#table-of-contents)**

## Objects and Data Structures

## オブジェクトとデータ構造

### Use getters and setters

### getter と setter を使う

TypeScript supports getter/setter syntax.
Using getters and setters to access data from objects that encapsulate behavior could be better that simply looking for a property on an object.
"Why?" you might ask. Well, here's a list of reasons:

* When you want to do more beyond getting an object property, you don't have to look up and change every accessor in your codebase.
* Makes adding validation simple when doing a *set*.
* Encapsulates the internal representation.
* Easy to add logging and error handling when getting and setting.
* You can lazy load your object's properties, let's say getting it from a server.

TypeScriptはgetter/setter構文をサポートしています。
getterとsetterを使って振る舞いをカプセル化してオブジェクトにアクセスするほうが、単純なプロパティでオブジェクトにアクセスするよいも優れている可能性があります。
「何故？」と思われるかもしれませんが、以下がその理由の一覧です:

* もしオブジェクトのプロパティを取得する以上のことをしてる場合、コード内のすべてのアクセサを調べて変更する必要がありません。
* *set* を使うとバリデーションが追加できます。
* 内部をカプセル化できます。
* 値を取得や設定する時にログやエラー処理を追加するのが容易になります。
* オブジェクトのプロパティを遅延ロードすることができるようになります、例えばサーバから値を取得する時などです。

**Bad:**

```ts
type BankAccount = {
  balance: number;
  // ...
}

const value = 100;
const account: BankAccount = { 
  balance: 0,
  // ... 
};

if (value < 0) {
  throw new Error('Cannot set negative balance.');
}

account.balance = value;
```

**Good:**

```ts
class BankAccount {
  private accountBalance: number = 0;

  get balance(): number {
    return this.accountBalance;
  }

  set balance(value: number) {
    if (value < 0) {
      throw new Error('Cannot set negative balance.');
    }

    this.accountBalance = value;
  }

  // ...
}

// Now `BankAccount` encapsulates the validation logic.
// If one day the specifications change, and we need extra validation rule,
// we would have to alter only the `setter` implementation, 
// leaving all dependent code unchanged. 
// これで `BankAccount` はバリデーション処理をカプセル化しました。
// ある日仕様が弁口されて、追加のバリデーションが必要になった場合にも
// `setter`の実装だけを変更すればよく
// すべての依存したコードを変更する必要はありません。
const account = new BankAccount();
account.balance = 100;
```

**[⬆ back to top](#table-of-contents)**

### Make objects have private/protected members

### オブジェクトにprivate/protectedメンバーをもたせる

TypeScript supports `public` *(default)*, `protected` and `private` accessors on class members.  

TypeScriptはクラスメンバーに対して`public`、*(default)*、`protected`、`private` アクセサをサポートしています。

**Bad:**

```ts
class Circle {
  radius: number;
  
  constructor(radius: number) {
    this.radius = radius;
  }

  perimeter() {
    return 2 * Math.PI * this.radius;
  }

  surface() {
    return Math.PI * this.radius * this.radius;
  }
}
```

**Good:**

```ts
class Circle {
  constructor(private readonly radius: number) {
  }

  perimeter() {
    return 2 * Math.PI * this.radius;
  }

  surface() {
    return Math.PI * this.radius * this.radius;
  }
}
```

**[⬆ back to top](#table-of-contents)**

### Prefer immutability

### 普遍性を好む

TypeScript's type system allows you to mark individual properties on an interface / class as *readonly*. This allows you to work in a functional way (unexpected mutation is bad).  
For more advanced scenarios there is a built-in type `Readonly` that takes a type `T` and marks all of its properties as readonly using mapped types (see [mapped types](https://www.typescriptlang.org/docs/handbook/advanced-types.html#mapped-types)).

TypeScriptの型システムではインタフェース/クラスのプロパティに *readonly* とマークすることができます。
これを用いると、あなたは関数型で書くことができるようになります。
(予想外の変更が良くないものです)
より高度なシナリオでは、組み込み型の `Readonly` があります。これは`T` 型 と map型を併用してすべてのプロパティを読み取り専用としてマークします。
([マップ型](https://www.typescriptlang.org/docs/handbook/advanced-types.html#mapped-types)を参照)

**Bad:**

```ts
interface Config {
  host: string;
  port: string;
  db: string;
}
```

**Good:**

```ts
interface Config {
  readonly host: string;
  readonly port: string;
  readonly db: string;
}
```

**[⬆ back to top](#table-of-contents)**

## Classes

### Classes should be small

The class' size is measured by it's responsibility. Following the *Single Responsibility principle* a class should be small.

**Bad:**

```ts
class Dashboard {
  getLanguage(): string { /* ... */ }
  setLanguage(language: string): void { /* ... */ }
  showProgress(): void { /* ... */ }
  hideProgress(): void { /* ... */ }
  isDirty(): boolean { /* ... */ }
  disable(): void { /* ... */ }
  enable(): void { /* ... */ }
  addSubscription(subscription: Subscription): void { /* ... */ }
  removeSubscription(subscription: Subscription): void { /* ... */ }
  addUser(user: User): void { /* ... */ }
  removeUser(user: User): void { /* ... */ }
  goToHomePage(): void { /* ... */ }
  updateProfile(details: UserDetails): void { /* ... */ }
  getVersion(): string { /* ... */ }
  // ...
}

```

**Good:**

```ts
class Dashboard {
  disable(): void { /* ... */ }
  enable(): void { /* ... */ }
  getVersion(): string { /* ... */ }
}

// split the responsibilities by moving the remaining methods to other classes
// ...
```

**[⬆ back to top](#table-of-contents)**

### High cohesion and low coupling

Cohesion defines the degree to which class members are related to each other. Ideally, all fields within a class should be used by each method.
We then say that the class is *maximally cohesive*. In practice, this however is not always possible, nor even advisable. You should however prefer cohesion to be high.  

Coupling refers to how related or dependent are two classes toward each other. Classes are said to be low coupled if changes in one of them doesn't affect the other one.  
  
Good software design has **high cohesion** and **low coupling**.

**Bad:**

```ts
class UserManager {
  // Bad: each private variable is used by one or another group of methods.
  // It makes clear evidence that the class is holding more than a single responsibility.
  // If I need only to create the service to get the transactions for a user,
  // I'm still forced to pass and instance of `emailSender`.
  constructor(
    private readonly db: Database,
    private readonly emailSender: EmailSender) {
  }

  async getUser(id: number): Promise<User> {
    return await db.users.findOne({ id });
  }

  async getTransactions(userId: number): Promise<Transaction[]> {
    return await db.transactions.find({ userId });
  }

  async sendGreeting(): Promise<void> {
    await emailSender.send('Welcome!');
  }

  async sendNotification(text: string): Promise<void> {
    await emailSender.send(text);
  }

  async sendNewsletter(): Promise<void> {
    // ...
  }
}
```

**Good:**

```ts
class UserService {
  constructor(private readonly db: Database) {
  }

  async getUser(id: number): Promise<User> {
    return await this.db.users.findOne({ id });
  }

  async getTransactions(userId: number): Promise<Transaction[]> {
    return await this.db.transactions.find({ userId });
  }
}

class UserNotifier {
  constructor(private readonly emailSender: EmailSender) {
  }

  async sendGreeting(): Promise<void> {
    await this.emailSender.send('Welcome!');
  }

  async sendNotification(text: string): Promise<void> {
    await this.emailSender.send(text);
  }

  async sendNewsletter(): Promise<void> {
    // ...
  }
}
```

**[⬆ back to top](#table-of-contents)**

### Prefer composition over inheritance

As stated famously in [Design Patterns](https://en.wikipedia.org/wiki/Design_Patterns) by the Gang of Four, you should *prefer composition over inheritance* where you can. There are lots of good reasons to use inheritance and lots of good reasons to use composition. The main point for this maxim is that if your mind instinctively goes for inheritance, try to think if composition could model your problem better. In some cases it can.  
  
You might be wondering then, "when should I use inheritance?" It depends on your problem at hand, but this is a decent list of when inheritance makes more sense than composition:

1. Your inheritance represents an "is-a" relationship and not a "has-a" relationship (Human->Animal vs. User->UserDetails).

2. You can reuse code from the base classes (Humans can move like all animals).

3. You want to make global changes to derived classes by changing a base class. (Change the caloric expenditure of all animals when they move).

**Bad:**

```ts
class Employee {
  constructor(
    private readonly name: string,
    private readonly email: string) {
  }

  // ...
}

// Bad because Employees "have" tax data. EmployeeTaxData is not a type of Employee
class EmployeeTaxData extends Employee {
  constructor(
    name: string,
    email: string,
    private readonly ssn: string,
    private readonly salary: number) {
    super(name, email);
  }

  // ...
}
```

**Good:**

```ts
class Employee {
  private taxData: EmployeeTaxData;

  constructor(
    private readonly name: string,
    private readonly email: string) {
  }

  setTaxData(ssn: string, salary: number): Employee {
    this.taxData = new EmployeeTaxData(ssn, salary);
    return this;
  }

  // ...
}

class EmployeeTaxData {
  constructor(
    public readonly ssn: string, 
    public readonly salary: number) {
  }

  // ...
}
```

**[⬆ back to top](#table-of-contents)**

### Use method chaining

This pattern is very useful and commonly used in many libraries. It allows your code to be expressive, and less verbose. For that reason, use method chaining and take a look at how clean your code will be.

**Bad:**

```ts
class QueryBuilder {
  private collection: string;
  private pageNumber: number = 1;
  private itemsPerPage: number = 100;
  private orderByFields: string[] = [];

  from(collection: string): void {
    this.collection = collection;
  }

  page(number: number, itemsPerPage: number = 100): void {
    this.pageNumber = number;
    this.itemsPerPage = itemsPerPage;
  }

  orderBy(...fields: string[]): void {
    this.orderByFields = fields;
  }

  build(): Query {
    // ...
  }
}

// ...

const queryBuilder = new QueryBuilder();
queryBuilder.from('users');
queryBuilder.page(1, 100);
queryBuilder.orderBy('firstName', 'lastName');

const query = queryBuilder.build();
```

**Good:**

```ts
class QueryBuilder {
  private collection: string;
  private pageNumber: number = 1;
  private itemsPerPage: number = 100;
  private orderByFields: string[] = [];

  from(collection: string): this {
    this.collection = collection;
    return this;
  }

  page(number: number, itemsPerPage: number = 100): this {
    this.pageNumber = number;
    this.itemsPerPage = itemsPerPage;
    return this;
  }

  orderBy(...fields: string[]): this {
    this.orderByFields = fields;
    return this;
  }

  build(): Query {
    // ...
  }
}

// ...

const query = new QueryBuilder()
  .from('users')
  .page(1, 100)
  .orderBy('firstName', 'lastName')
  .build();
```

**[⬆ back to top](#table-of-contents)**

## SOLID

### Single Responsibility Principle (SRP)

As stated in Clean Code, "There should never be more than one reason for a class to change". It's tempting to jam-pack a class with a lot of functionality, like when you can only take one suitcase on your flight. The issue with this is that your class won't be conceptually cohesive and it will give it many reasons to change. Minimizing the amount of times you need to change a class is important. It's important because if too much functionality is in one class and you modify a piece of it, it can be difficult to understand how that will affect other dependent modules in your codebase.

**Bad:**

```ts
class UserSettings {
  constructor(private readonly user: User) {
  }

  changeSettings(settings: UserSettings) {
    if (this.verifyCredentials()) {
      // ...
    }
  }

  verifyCredentials() {
    // ...
  }
}
```

**Good:**

```ts
class UserAuth {
  constructor(private readonly user: User) {
  }

  verifyCredentials() {
    // ...
  }
}


class UserSettings {
  private readonly auth: UserAuth;

  constructor(private readonly user: User) {
    this.auth = new UserAuth(user);
  }

  changeSettings(settings: UserSettings) {
    if (this.auth.verifyCredentials()) {
      // ...
    }
  }
}
```

**[⬆ back to top](#table-of-contents)**

### Open/Closed Principle (OCP)

As stated by Bertrand Meyer, "software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification." What does that mean though? This principle basically states that you should allow users to add new functionalities without changing existing code.

**Bad:**

```ts
class AjaxAdapter extends Adapter {
  constructor() {
    super();
  }

  // ...
}

class NodeAdapter extends Adapter {
  constructor() {
    super();
  }

  // ...
}

class HttpRequester {
  constructor(private readonly adapter: Adapter) {
  }

  async fetch<T>(url: string): Promise<T> {
    if (this.adapter instanceof AjaxAdapter) {
      const response = await makeAjaxCall<T>(url);
      // transform response and return
    } else if (this.adapter instanceof NodeAdapter) {
      const response = await makeHttpCall<T>(url);
      // transform response and return
    }
  }
}

function makeAjaxCall<T>(url: string): Promise<T> {
  // request and return promise
}

function makeHttpCall<T>(url: string): Promise<T> {
  // request and return promise
}
```

**Good:**

```ts
abstract class Adapter {
  abstract async request<T>(url: string): Promise<T>;

  // code shared to subclasses ...
}

class AjaxAdapter extends Adapter {
  constructor() {
    super();
  }

  async request<T>(url: string): Promise<T>{
    // request and return promise
  }

  // ...
}

class NodeAdapter extends Adapter {
  constructor() {
    super();
  }

  async request<T>(url: string): Promise<T>{
    // request and return promise
  }

  // ...
}

class HttpRequester {
  constructor(private readonly adapter: Adapter) {
  }

  async fetch<T>(url: string): Promise<T> {
    const response = await this.adapter.request<T>(url);
    // transform response and return
  }
}
```

**[⬆ back to top](#table-of-contents)**

### Liskov Substitution Principle (LSP)

This is a scary term for a very simple concept. It's formally defined as "If S is a subtype of T, then objects of type T may be replaced with objects of type S (i.e., objects of type S may substitute objects of type T) without altering any of the desirable properties of that program (correctness, task performed, etc.)." That's an even scarier definition.  
  
The best explanation for this is if you have a parent class and a child class, then the base class and child class can be used interchangeably without getting incorrect results. This might still be confusing, so let's take a look at the classic Square-Rectangle example. Mathematically, a square is a rectangle, but if you model it using the "is-a" relationship via inheritance, you quickly get into trouble.

**Bad:**

```ts
class Rectangle {
  constructor(
    protected width: number = 0,
    protected height: number = 0) {

  }

  setColor(color: string): this {
    // ...
  }

  render(area: number) {
    // ...
  }

  setWidth(width: number): this {
    this.width = width;
    return this;
  }

  setHeight(height: number): this {
    this.height = height;
    return this;
  }

  getArea(): number {
    return this.width * this.height;
  }
}

class Square extends Rectangle {
  setWidth(width: number): this {
    this.width = width;
    this.height = width;
    return this;
  }

  setHeight(height: number): this {
    this.width = height;
    this.height = height;
    return this;
  }
}

function renderLargeRectangles(rectangles: Rectangle[]) {
  rectangles.forEach((rectangle) => {
    const area = rectangle
      .setWidth(4)
      .setHeight(5)
      .getArea(); // BAD: Returns 25 for Square. Should be 20.
    rectangle.render(area);
  });
}

const rectangles = [new Rectangle(), new Rectangle(), new Square()];
renderLargeRectangles(rectangles);
```

**Good:**

```ts
abstract class Shape {
  setColor(color: string): this {
    // ...
  }

  render(area: number) {
    // ...
  }

  abstract getArea(): number;
}

class Rectangle extends Shape {
  constructor(
    private readonly width = 0,
    private readonly height = 0) {
    super();
  }

  getArea(): number {
    return this.width * this.height;
  }
}

class Square extends Shape {
  constructor(private readonly length: number) {
    super();
  }

  getArea(): number {
    return this.length * this.length;
  }
}

function renderLargeShapes(shapes: Shape[]) {
  shapes.forEach((shape) => {
    const area = shape.getArea();
    shape.render(area);
  });
}

const shapes = [new Rectangle(4, 5), new Rectangle(4, 5), new Square(5)];
renderLargeShapes(shapes);
```

**[⬆ back to top](#table-of-contents)**

### Interface Segregation Principle (ISP)

ISP states that "Clients should not be forced to depend upon interfaces that they do not use.". This principle is very much related to the Single Responsibility Principle.
What it really means is that you should always design your abstractions in a way that the clients that are using the exposed methods do not get the whole pie instead. That also include imposing the clients with the burden of implementing methods that they don’t actually need.

**Bad:**

```ts
interface SmartPrinter {
  print();
  fax();
  scan();
}

class AllInOnePrinter implements SmartPrinter {
  print() {
    // ...
  }  
  
  fax() {
    // ...
  }

  scan() {
    // ...
  }
}

class EconomicPrinter implements SmartPrinter {
  print() {
    // ...
  }  
  
  fax() {
    throw new Error('Fax not supported.');
  }

  scan() {
    throw new Error('Scan not supported.');
  }
}
```

**Good:**

```ts
interface Printer {
  print();
}

interface Fax {
  fax();
}

interface Scanner {
  scan();
}

class AllInOnePrinter implements Printer, Fax, Scanner {
  print() {
    // ...
  }  
  
  fax() {
    // ...
  }

  scan() {
    // ...
  }
}

class EconomicPrinter implements Printer {
  print() {
    // ...
  }
}
```

**[⬆ back to top](#table-of-contents)**

### Dependency Inversion Principle (DIP)

This principle states two essential things:

1. High-level modules should not depend on low-level modules. Both should depend on abstractions.

2. Abstractions should not depend upon details. Details should depend on abstractions.

This can be hard to understand at first, but if you've worked with Angular, you've seen an implementation of this principle in the form of Dependency Injection (DI). While they are not identical concepts, DIP keeps high-level modules from knowing the details of its low-level modules and setting them up. It can accomplish this through DI. A huge benefit of this is that it reduces the coupling between modules. Coupling is a very bad development pattern because it makes your code hard to refactor.  
  
DIP is usually achieved by a using an inversion of control (IoC) container. An example of a powerful IoC container for TypeScript is [InversifyJs](https://www.npmjs.com/package/inversify)

**Bad:**

```ts
import { readFile as readFileCb } from 'fs';
import { promisify } from 'util';

const readFile = promisify(readFileCb);

type ReportData = {
  // ..
}

class XmlFormatter {
  parse<T>(content: string): T {
    // Converts an XML string to an object T
  }
}

class ReportReader {

  // BAD: We have created a dependency on a specific request implementation.
  // We should just have ReportReader depend on a parse method: `parse`
  private readonly formatter = new XmlFormatter();

  async read(path: string): Promise<ReportData> {
    const text = await readFile(path, 'UTF8');
    return this.formatter.parse<ReportData>(text);
  }
}

// ...
const reader = new ReportReader();
await report = await reader.read('report.xml');
```

**Good:**

```ts
import { readFile as readFileCb } from 'fs';
import { promisify } from 'util';

const readFile = promisify(readFileCb);

type ReportData = {
  // ..
}

interface Formatter {
  parse<T>(content: string): T;
}

class XmlFormatter implements Formatter {
  parse<T>(content: string): T {
    // Converts an XML string to an object T
  }
}


class JsonFormatter implements Formatter {
  parse<T>(content: string): T {
    // Converts a JSON string to an object T
  }
}

class ReportReader {
  constructor(private readonly formatter: Formatter) {
  }

  async read(path: string): Promise<ReportData> {
    const text = await readFile(path, 'UTF8');
    return this.formatter.parse<ReportData>(text);
  }
}

// ...
const reader = new ReportReader(new XmlFormatter());
await report = await reader.read('report.xml');

// or if we had to read a json report
const reader = new ReportReader(new JsonFormatter());
await report = await reader.read('report.json');
```

**[⬆ back to top](#table-of-contents)**

## Testing

Testing is more important than shipping. If you have no tests or an inadequate amount, then every time you ship code you won't be sure that you didn't break anything.
Deciding on what constitutes an adequate amount is up to your team, but having 100% coverage (all statements and branches)
is how you achieve very high confidence and developer peace of mind. This means that in addition to having a great testing framework, you also need to use a good coverage tool.

There's no excuse to not write tests. There are plenty of good JS test frameworks with typings support for TypeScript, so find one that your team prefers. When you find one that works for your team, then aim to always write tests for every new feature/module you introduce. If your preferred method is Test Driven Development (TDD), that is great, but the main point is to just make sure you are reaching your coverage goals before launching any feature, or refactoring an existing one.  

### The three laws of TDD

1. You are not allowed to write any production code unless it is to make a failing unit test pass.

2. You are not allowed to write any more of a unit test than is sufficient to fail; and compilation failures are failures.

3. You are not allowed to write any more production code than is sufficient to pass the one failing unit test.

**[⬆ back to top](#table-of-contents)**

### F.I.R.S.T. rules

Clean tests should follow the rules:

* **Fast** tests should be fast because we want to run them frequently.

* **Independent** tests should not depend on each other. They should provide same output whether run independently or all together in any order.

* **Repeatable** tests should be repeatable in any environment and there should be no excuse for why they fail.

* **Self-Validating** a test should answer with either *Passed* or *Failed*. You don't need to compare log files to answer if a test passed.

* **Timely** unit tests should be written before the production code. If you write tests after the production code, you might find writing tests too hard.

**[⬆ back to top](#table-of-contents)**

### Single concept per test

Tests should also follow the *Single Responsibility Principle*. Make only one assert per unit test.

**Bad:**

```ts
import { assert } from 'chai';

describe('AwesomeDate', () => {
  it('handles date boundaries', () => {
    let date: AwesomeDate;

    date = new AwesomeDate('1/1/2015');
    assert.equal('1/31/2015', date.addDays(30));

    date = new AwesomeDate('2/1/2016');
    assert.equal('2/29/2016', date.addDays(28));

    date = new AwesomeDate('2/1/2015');
    assert.equal('3/1/2015', date.addDays(28));
  });
});
```

**Good:**

```ts
import { assert } from 'chai';

describe('AwesomeDate', () => {
  it('handles 30-day months', () => {
    const date = new AwesomeDate('1/1/2015');
    assert.equal('1/31/2015', date.addDays(30));
  });

  it('handles leap year', () => {
    const date = new AwesomeDate('2/1/2016');
    assert.equal('2/29/2016', date.addDays(28));
  });

  it('handles non-leap year', () => {
    const date = new AwesomeDate('2/1/2015');
    assert.equal('3/1/2015', date.addDays(28));
  });
});
```

**[⬆ back to top](#table-of-contents)**

### The name of the test should reveal it's intention

When a test fail, it's name is the first indication of what may have gone wrong.

**Bad:**

```ts
describe('Calendar', () => {
  it('2/29/2020', () => {
    // ...
  });

  it('throws', () => {
    // ...
  });
});
```

**Good:**

```ts
describe('Calendar', () => {
  it('should handle leap year', () => {
    // ...
  });

  it('should throw when format is invalid', () => {
    // ...
  });
});
```

**[⬆ back to top](#table-of-contents)**

## Concurrency

### Prefer promises vs callbacks

Callbacks aren't clean, and they cause excessive amounts of nesting *(the callback hell)*.  
There are utilities that transform existing functions using the callback style to a version that returns promises
(for Node.js see [`util.promisify`](https://nodejs.org/dist/latest-v8.x/docs/api/util.html#util_util_promisify_original), for general purpose see [pify](https://www.npmjs.com/package/pify), [es6-promisify](https://www.npmjs.com/package/es6-promisify))

**Bad:**

```ts
import { get } from 'request';
import { writeFile } from 'fs';

function downloadPage(url: string, saveTo: string, callback: (error: Error, content?: string) => void) {
  get(url, (error, response) => {
    if (error) {
      callback(error);
    } else {
      writeFile(saveTo, response.body, (error) => {
        if (error) {
          callback(error);
        } else {
          callback(null, response.body);
        }
      });
    }
  });
}

downloadPage('https://en.wikipedia.org/wiki/Robert_Cecil_Martin', 'article.html', (error, content) => {
  if (error) {
    console.error(error);
  } else {
    console.log(content);
  }
});
```

**Good:**

```ts
import { get } from 'request';
import { writeFile } from 'fs';
import { promisify } from 'util';

const write = promisify(writeFile);

function downloadPage(url: string, saveTo: string): Promise<string> {
  return get(url)
    .then(response => write(saveTo, response));
}

downloadPage('https://en.wikipedia.org/wiki/Robert_Cecil_Martin', 'article.html')
  .then(content => console.log(content))
  .catch(error => console.error(error));  
```

Promises supports a few helper methods that help make code more conscise:  

| Pattern                  | Description                                |  
| ------------------------ | -----------------------------------------  |  
| `Promise.resolve(value)` | Convert a value into a resolved promise.   |  
| `Promise.reject(error)`  | Convert an error into a rejected promise.  |  
| `Promise.all(promises)`  |Returns a new promise which is fulfilled with an array of fulfillment values for the passed promises or rejects with the reason of the first promise that rejects. |
| `Promise.race(promises)`|Returns a new promise which is fulfilled/rejected with the result/error of the first settled promise from the array of passed promises. |

`Promise.all` is especially useful when there is a need to run tasks in parallel. `Promise.race` makes it easier to implement things like timeouts for promises.

**[⬆ back to top](#table-of-contents)**

### Async/Await are even cleaner than Promises

With `async`/`await` syntax you can write code that is far cleaner and more understandable that chained promises. Within a function prefixed with `async` keyword you have a way to tell the JavaScript runtime to pause the execution of code on the `await` keyword (when used on a promise).

**Bad:**

```ts
import { get } from 'request';
import { writeFile } from 'fs';
import { promisify } from 'util';

const write = util.promisify(writeFile);

function downloadPage(url: string, saveTo: string): Promise<string> {
  return get(url).then(response => write(saveTo, response));
}

downloadPage('https://en.wikipedia.org/wiki/Robert_Cecil_Martin', 'article.html')
  .then(content => console.log(content))
  .catch(error => console.error(error));  
```

**Good:**

```ts
import { get } from 'request';
import { writeFile } from 'fs';
import { promisify } from 'util';

const write = promisify(writeFile);

async function downloadPage(url: string, saveTo: string): Promise<string> {
  const response = await get(url);
  await write(saveTo, response);
  return response;
}

// somewhere in an async function
try {
  const content = await downloadPage('https://en.wikipedia.org/wiki/Robert_Cecil_Martin', 'article.html');
  console.log(content);
} catch (error) {
  console.error(error);
}
```

**[⬆ back to top](#table-of-contents)**

## Error Handling

## エラー処理

Thrown errors are a good thing! They mean the runtime has successfully identified when something in your program has gone wrong and it's letting you know by stopping function
execution on the current stack, killing the process (in Node), and notifying you in the console with a stack trace.

例外が発生するのは良いことです！
これはプログラムの何かが正常に動作しなかった事をランタイムが正常に判別出来たことを意味します。
そして現在のスタックで関数の実行を停止して（Node内の）プロセスを強制終了し、コンソールにスタックトレースを表示して通知します。

### Always use Error for throwing or rejecting

### ThrowやRejectの時にErrorを使う

JavaScript as well as TypeScript allow you to `throw` any object. A Promise can also be rejected with any reason object. 

JavaScriptとTypeScriptは任意のオブジェクトを `throw` できます。
Promiseの場合は `reject` することができます。

It is advisable to use the `throw` syntax with an `Error` type. This is because your error might be caught in higher level code with a `catch` syntax.
It would be very confusing to catch a string message there and would make
[debugging more painful](https://basarat.gitbooks.io/typescript/docs/types/exceptions.html#always-use-error).  
For the same reason you should reject promises with `Error` types.

`Error` 型と `throw` 構文を使うようにしましょう。
これは貴方のエラーが `catch` 構文を使ってより高いレベルのコードで補足されるかもしれないからです。
その時に文字列でメッセージを出すのはとても混乱を招くでしょう。
[より厄介なデバッグ](https://basarat.gitbooks.io/typescript/docs/types/exceptions.html#always-use-error)
同じ理由で `Error` 型の `reject` を行うべきです。

**Bad:**

```ts
function calculateTotal(items: Item[]): number {
  throw 'Not implemented.';
}

function get(): Promise<Item[]> {
  return Promise.reject('Not implemented.');
}
```

**Good:**

```ts
function calculateTotal(items: Item[]): number {
  throw new Error('Not implemented.');
}

function get(): Promise<Item[]> {
  return Promise.reject(new Error('Not implemented.'));
}

// or equivalent to:

async function get(): Promise<Item[]> {
  throw new Error('Not implemented.');
}
```

The benefit of using `Error` types is that it is supported by the syntax `try/catch/finally` and implicitly all errors have the `stack` property which
is very powerful for debugging.  
There are also another alternatives, not to use the `throw` syntax and instead always return custom error objects. TypeScript makes this even easier.
Consider following example:

`Error` 型を使う利点は、それが `try/catch/finally` 構文によってサポートされており、暗黙的に `stack` プロパティを持つためデバッグにおいて非常に強力だからです。
`throw` 構文を使わずに常にカスタムエラーオブジェクトを返すという方法もあります。
TypeScriptはそれを更に簡単にします。
次の例を参考にしてみてください：

```ts
type Result<R> = { isError: false, value: R };
type Failure<E> = { isError: true, error: E };
type Failable<R, E> = Result<R> | Failure<E>;

function calculateTotal(items: Item[]): Failable<number, 'empty'> {
  if (items.length === 0) {
    return { isError: true, error: 'empty' };
  }

  // ...
  return { isError: false, value: 42 };
}
```

For the detailed explanation of this idea refer to the [original post](https://medium.com/@dhruvrajvanshi/making-exceptions-type-safe-in-typescript-c4d200ee78e9).

このアイディアの詳細については[元の記事](https://medium.com/@dhruvrajvanshi/making-exceptions-type-safe-in-typescript-c4d200ee78e9)を参照してください。

**[⬆ back to top](#table-of-contents)**

### Don't ignore caught errors

### 例外を握りつぶさない

Doing nothing with a caught error doesn't give you the ability to ever fix or react to said error. Logging the error to the console (`console.log`) isn't much better as often times it can get lost in a sea of things printed to the console. If you wrap any bit of code in a `try/catch` it means you think an error may occur there and therefore you should have a plan, or create a code path, for when it occurs.

捉えられた例外に対して何もしないというのは、例外が発生しても例外を発見したり、修正することができなくなります。
コンソール (`console.log`)にエラーを表示するのは、頻繁にコーンソール表示の海に溺れてしまうためあまり良いことではありません。
コードの一部でも `try/catch` で囲むとそこでエラーが発生する可能性があり、発生したエラーに備えた計画を立て、例外が発生したときのコードパスを作る必要があります。

**Bad:**

```ts
try {
  functionThatMightThrow();
} catch (error) {
  console.log(error);
}

// or even worse

try {
  functionThatMightThrow();
} catch (error) {
  // ignore error
}
```

**Good:**

```ts
import { logger } from './logging'

try {
  functionThatMightThrow();
} catch (error) {
  logger.log(error);
}
```

**[⬆ back to top](#table-of-contents)**

### Don't ignore rejected promises

### reject された promise を無視しない

For the same reason you shouldn't ignore caught errors from `try/catch`.

同じ理由で、`try/catch` された例外を無視してはいけません。

**Bad:**

```ts
getUser()
  .then((user: User) => {
    return sendEmail(user.email, 'Welcome!');
  })
  .catch((error) => {
    console.log(error);
  });
```

**Good:**

```ts
import { logger } from './logging'

getUser()
  .then((user: User) => {
    return sendEmail(user.email, 'Welcome!');
  })
  .catch((error) => {
    logger.log(error);
  });

// or using the async/await syntax:
// もしくは async/await 構文を使う

try {
  const user = await getUser();
  await sendEmail(user.email, 'Welcome!');
} catch (error) {
  logger.log(error);
}
```

**[⬆ back to top](#table-of-contents)**

## Formatting

## フォーマット

Formatting is subjective. Like many rules herein, there is no hard and fast rule that you must follow. The main point is *DO NOT ARGUE* over formatting. There are tons of tools to automate this. Use one! It's a waste of time and money for engineers to argue over formatting. The general rule to follow is *keep consistent formatting rules*.  

フォーマットは主観的です。
ここにある多くの規則のように、貴方が従わなければならない厳しく厳密なルールではありません。
重要な点は、フォーマットについて *論議しないこと* です。
これを自動化するツールはたくさんあります。
それを使ってくさい。
エンジニアがフォーマットについて論議するのは時間とお金の無駄です。
従うべき一般的な規則は *一貫したフォーマットルールを守る* ことです。

For TypeScript there is a powerful tool called [TSLint](https://palantir.github.io/tslint/). It's a static analysis tool that can help you improve dramatically the readability and maintainability of your code. There are ready to use TSLint configurations that you can reference in your projects:

TypeScriptには[TSLint](https://palantir.github.io/tslint/)という強力なツールがあります。
コードの読みやすさと保守性を劇的に向上させるのに役立つ静的分析ツールです。
プロジェクトですぐに使えるTSLint構成です：

* [TSLint Config Standard](https://www.npmjs.com/package/tslint-config-standard) - standard style rules

* [TSLint Config Airbnb](https://www.npmjs.com/package/tslint-config-airbnb) - Airbnb style guide

* [TSLint Clean Code](https://www.npmjs.com/package/tslint-clean-code) - TSLint rules inspired by the [Clean Code: A Handbook of Agile Software Craftsmanship](https://www.amazon.ca/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)

* [TSLint react](https://www.npmjs.com/package/tslint-react) - lint rules related to React & JSX

* [TSLint + Prettier](https://www.npmjs.com/package/tslint-config-prettier) - lint rules for [Prettier](https://github.com/prettier/prettier) code formatter

* [ESLint rules for TSLint](https://www.npmjs.com/package/tslint-eslint-rules) - ESLint rules for TypeScript

* [Immutable](https://www.npmjs.com/package/tslint-immutable) - rules to disable mutation in TypeScript

Refer also to this great [TypeScript StyleGuide and Coding Conventions](https://basarat.gitbooks.io/typescript/docs/styleguide/styleguide.html) source.

[TypeScriptスタイルガイドとコーディング規約](https://basarat.gitbooks.io/typescript/docs/styleguide/styleguide.html)も参照してください。

### Use consistent capitalization

### 一貫性を持った大文字を使用すること

Capitalization tells you a lot about your variables, functions, etc. These rules are subjective, so your team can choose whatever they want. The point is, no matter what you all choose, just *be consistent*.

大文字と小文字は変数や関数について多くのことを教えてくれます。
このルールは主観的なものなので、チームは必要に応じて好きなものを選ぶことができます。
重要なのは貴方が選んだどんなことであってもシンプルに *一貫性を持つ* ことです。

**Bad:**

```ts
const DAYS_IN_WEEK = 7;
const daysInMonth = 30;

const songs = ['Back In Black', 'Stairway to Heaven', 'Hey Jude'];
const Artists = ['ACDC', 'Led Zeppelin', 'The Beatles'];

function eraseDatabase() {}
function restore_database() {}

type animal { /* ... */ }
type Container { /* ... */ }
```

**Good:**

```ts
const DAYS_IN_WEEK = 7;
const DAYS_IN_MONTH = 30;

const SONGS = ['Back In Black', 'Stairway to Heaven', 'Hey Jude'];
const ARTISTS = ['ACDC', 'Led Zeppelin', 'The Beatles'];

function eraseDatabase() {}
function restoreDatabase() {}

type Animal { /* ... */ }
type Container { /* ... */ }
```

Prefer using `PascalCase` for class, interface, type and namespace names.  
Prefer using `camelCase` for variables, functions and class members.

クラス、インタフェース、タイプ、名前空間には `PascalCase` の利用が好ましいでしょう。
変数、関数、クラスメンバーには `camelCase` が好ましいでしょう。

**[⬆ back to top](#table-of-contents)**

### Function callers and callees should be close

### 関数の呼び出し元と定義は近いはずです。

If a function calls another, keep those functions vertically close in the source file. Ideally, keep the caller right above the callee.
We tend to read code from top-to-bottom, like a newspaper. Because of this, make your code read that way.

関数が別の関数を呼び出す場合は、それらの関数をソースファイル内のすぐ近くに定義してください。
理想的には、呼び出し元を定義の真上に置いてください。
私たちは新聞のように上から下へとコードを読みます。
このため、あなたのコードもそのように読めるようにします。

**Bad:**

```ts
class PerformanceReview {
  constructor(private readonly employee: Employee) {
  }

  private lookupPeers() {
    return db.lookup(this.employee.id, 'peers');
  }

  private lookupManager() {
    return db.lookup(this.employee, 'manager');
  }

  private getPeerReviews() {
    const peers = this.lookupPeers();
    // ...
  }

  review() {
    this.getPeerReviews();
    this.getManagerReview();
    this.getSelfReview();

    // ...
  }

  private getManagerReview() {
    const manager = this.lookupManager();
  }

  private getSelfReview() {
    // ...
  }
}

const review = new PerformanceReview(employee);
review.review();
```

**Good:**

```ts
class PerformanceReview {
  constructor(private readonly employee: Employee) {
  }

  review() {
    this.getPeerReviews();
    this.getManagerReview();
    this.getSelfReview();

    // ...
  }

  private getPeerReviews() {
    const peers = this.lookupPeers();
    // ...
  }

  private lookupPeers() {
    return db.lookup(this.employee.id, 'peers');
  }

  private getManagerReview() {
    const manager = this.lookupManager();
  }

  private lookupManager() {
    return db.lookup(this.employee, 'manager');
  } 

  private getSelfReview() {
    // ...
  }
}

const review = new PerformanceReview(employee);
review.review();
```

**[⬆ back to top](#table-of-contents)**

### type vs. interface

### タイプ VS インタフェース

Use type when you might need a union or intersection. Use interface when you want `extends` or `implements`. There is no strict rule however, use the one that works for you.  
For a more detailed explanation refer to this [answer](https://stackoverflow.com/questions/37233735/typescript-interfaces-vs-types/54101543#54101543) about the differences between `type` and `interface` in TypeScript.

union や intersection が必要な場合は type を使用してください。
extends や impliments がほしいときにはinterfaceを使います。
厳密なルールはありませんが、その時に合ったものを使ってください。
TypeScriptの `type` と `interface` の違いについてのより詳細な説明はこちらの [回答](https://stackoverflow.com/questions/37233735/typescript-interfaces-vs-types/54101543#54101543) を参照してください。

**Bad:**

```ts
interface EmailConfig {
  // ...
}

interface DbConfig {
  // ...
}

interface Config {
  // ...
}

//...

type Shape {
  // ...
}
```

**Good:**

```ts

type EmailConfig {
  // ...
}

type DbConfig {
  // ...
}

type Config  = EmailConfig | DbConfig;

// ...

interface Shape {
  // ...
}

class Circle implements Shape {
  // ...
}

class Square implements Shape {
  // ...
}
```

**[⬆ back to top](#table-of-contents)**

## Comments

## コメント

The use of a comments is an indication of failure to express without them. Code should be the only source of truth.

> Don’t comment bad code—rewrite it.  
> — *Brian W. Kernighan and P. J. Plaugher*

コメントを使用するのは、それなしでは表現できなかったことを表します。
コードが唯一の真実であるべきです。

> 悪いコードにコメントをしていないで書き換えてください。
> — *Brian W. Kernighan and P. J. Plaugher*

### Prefer self explanatory code instead of comments

### コメントではなく、自己説明的なコードを好む

Comments are an apology, not a requirement. Good code mostly documents itself.

コメントは弁明であり、必須ではありません。
良いコードはほとんど文章のようになっています。

**Bad:**

```ts
// Check if subscription is active.
// subscriptionが有効かを確認
if (subscription.endDate > Date.now) {  }
```

**Good:**

```ts
const isSubscriptionActive = subscription.endDate > Date.now;
if (isSubscriptionActive) { /* ... */ }
```

**[⬆ back to top](#table-of-contents)**

### Don't leave commented out code in your codebase

### コメントアウトされたコードを残さない

Version control exists for a reason. Leave old code in your history.

バージョン管理ツールが存在する理由です、古いコードは履歴に残しましょう。

**Bad:**

```ts
type User = {
  name: string;
  email: string;
  // age: number;
  // jobPosition: string;
}
```

**Good:**

```ts
type User = {
  name: string;
  email: string;
}
```

**[⬆ back to top](#table-of-contents)**

### Don't have journal comments

### 日付を持ったコメントはいりません

Remember, use version control! There's no need for dead code, commented code, and especially journal comments. Use git log to get history!

バージョン管理ツールを使うことを覚えましょう！
使ってないコード、コメントアウトされたコード、日記のようなコメントは不要です。
gitの履歴を取得するのに git log を使ってください。

**Bad:**

```ts
/**
 * 2016-12-20: Removed monads, didn't understand them (RM)
 * 2016-10-01: Improved using special monads (JP)
 * 2016-02-03: Added type-checking (LI)
 * 2015-03-14: Implemented combine (JR)
 */
function combine(a: number, b: number): number {
  return a + b;
}
```

**Good:**

```ts
function combine(a: number, b: number): number {
  return a + b;
}
```

**[⬆ back to top](#table-of-contents)**

### Avoid positional markers

### 位置取りの印として使うのをさける

They usually just add noise. Let the functions and variable names along with the proper indentation and formatting give the visual structure to your code.  
Most IDE support code folding feature that allows you to collapse/expand blocks of code (see Visual Studio Code [folding regions](https://code.visualstudio.com/updates/v1_17#_folding-regions)).

これは単純にノイズです。
関数と変数名を適切なインデント、フォーマットで使用して、コードの視覚的な構造を持ちましょう。
これは単純にノイズです。
関数と変数名を適切なインデント、フォーマットで使用して、コードの視覚的な構造を持ちましょう。
ほとんどのIDEはコードの折りたたみ機能をサポートしているので、コードブロックを折りたたむ／展開することができます。(Visual Studio Code [folding regions](https://code.visualstudio.com/updates/v1_17#_folding-regions)を参照).

**Bad:**

```ts
////////////////////////////////////////////////////////////////////////////////
// Client class
////////////////////////////////////////////////////////////////////////////////
class Client {
  id: number;
  name: string;
  address: Address;
  contact: Contact;

  ////////////////////////////////////////////////////////////////////////////////
  // public methods
  ////////////////////////////////////////////////////////////////////////////////
  public describe(): string {
    // ...
  }

  ////////////////////////////////////////////////////////////////////////////////
  // private methods
  ////////////////////////////////////////////////////////////////////////////////
  private describeAddress(): string {
    // ...
  }

  private describeContact(): string {
    // ...
  }
};
```

**Good:**

```ts
class Client {
  id: number;
  name: string;
  address: Address;
  contact: Contact;

  public describe(): string {
    // ...
  }

  private describeAddress(): string {
    // ...
  }

  private describeContact(): string {
    // ...
  }
};
```

**[⬆ back to top](#table-of-contents)**
