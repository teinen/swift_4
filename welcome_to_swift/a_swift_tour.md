# The Swift Programming Language(Swift 4)
## A Swift Tour

伝統的に、新しい言語での最初のプログラムは「Hello, world!」と画面に出力することと決まっています。  
Swiftでは1行でそれが可能です。  

    print("Hello, world!")

もしあなたがC言語やObjective-Cを書いたことがあるなら、こういった記法には見覚えがあるかもしれませんが、  
Swiftではこの1行で完璧なコードとして機能します。I/Oや文字列操作等の機能的なImportは必要ありません。  
また、コードの最後にセミコロン(;)を置く必要もありません。

このツアーをこなすことで、あなたは様々なプログラム上の課題を解決する方法を学ぶことを通して、Swiftでコードを書くのに  
充分な情報を得ることが出来ます。  

<!-- 改ページ -->
<div style="page-break-before:always"></div>

### <u>Simple Value(単純な値)</u>
定数は `let` 、変数は `var` として宣言します。  
定数はコンパイル時には値が入っている必要はありませんが、必ず値を1度は定義しなければなりません。  

    var myVariable = 42  
    myVariable = 50  
    let myConstant = 42

定数及び変数に代入する値の「型」については、コンパイラによる**型推論**が働く為、必ずしも指定する必要はありません。  
もし代入された値が型推論に必要な情報を持っていない(例えば小数点が無い等)場合、明示的な型指定を行うことが可能です。  
明示的な型指定は `let 変数名: 型 = 値` のようにします。

    let implicitInteger = 70
    let implicitDouble = 70.0
    let ecplicitDouble: Double = 70.0

値の型において、暗黙の型変換は行われません。  
異なる型に変換したい場合は、明示的にキャストしなければなりません。

    let label = "The width is "
    let width = 94
    let widthLabel = label + String(width)

`let` や `var`で宣言した値を文字列の中に埋め込む方法は簡単です  
カッコの中に変数名を書き、バックスラッシュ(\\)をその前に付けるだけです。

    let apples = 3
    let oranges = 5
    let appleSummary = "I have \(apples) apples."
    let fruitSummary = "I have \(apples + oranges) pieces of fruit."

複数行の文字列を宣言したい場合は、ダブルクォートを3つ使用します(""")。  
ダブルクォートで囲まれた文字列の先頭にあるインデントは、終わりの引用符のインデントに一致する限り  
無視されます。

    let quotation = """
    この行の先頭にスペースやタブがあっても、実際は無視されます.
    インデントが適用されるのは、この行からです.
    3連引用符の中では、ダブルクォートはエスケープ無しで書けます(").
    """

配列(`arrays`)や辞書(`dictionaries`)を宣言するには、ブラケット([])を使用します。  
各要素へのアクセスはインデックスを使用します。  
配列や辞書の最終要素の後にはコンマがついてもかまいません。

    // 配列
    var shoppingList = ["catfish", "water", "tulips", "blue paint"]
    shoppingList[1] = "bottle of water"

    // 辞書
    var occupations = [
        "Malcolm: "Captain",
        "Kaylee": "Mechanic",
    ]
    occupatins["Jayne"] = "Public Relations"

空白の配列や辞書を宣言したい場合は、初期化構文を使用します。

    let emptyArray = [String]()
    let emptyDictionary = [String:Float]()

型推論が可能な場合、空白の配列や辞書を以下のように宣言することも出来ます。  
(例えば、変数に新たな値を設定したり、関数に引数を渡したりといった場面で使用します。)

    shoppingList = []
    occupatins = [:]

<!-- 改ページ -->
<div style="page-break-before:always"></div>

### <u>Control Flow(制御構文)</u>
条件分岐処理を実装する際は `if` や `switch` 、繰り返し処理を実装する際は `for-in` や `while` 、`repeat-while` を使用します。  

    let individualScores = [75, 43, 103, 87, 12]
    var teamScore = 0

    // for-in文での繰り返し処理
    for score in individualScores {
        // if文での条件分岐処理
        if score > 50 {
            teamScore += 3
        } else {
            teamScore += 1
        }
    }
    print(teamScore)

`if` 文の条件式での判定結果は、必ずBooleanでなくてはなりません。  
これは `if score { ... }` のような条件は、0との暗黙的な比較とは見なされず、エラーになることを示しています。

`if` と `let` は一緒に使用することで、`nil` (存在しないことを表す)の可能性がある値を扱うことが出来ます。  

そういった値( `nil` の可能性がある値)は、<u>**オプショナル型**</u>と表現されます。  
オプショナル型の値には、実際の値かもしくは、値が存在しないことを示す `nil` が含まれています。  
オプショナル型の値を宣言するには、型指定の後に `?` を付けます。

    var optionalString: String? = "Hello"

`if` と `let` を用いたオプショナル型の扱い方は `Optional Binding` と呼ばれます。

    var optionalName: String? = "John Appleseed"
    var greeting = "Hello!"

    // Optinal Binding
    if let name = optionalName {
        greeting = "Hello, \(name)"
    }

もしオプショナル型の値が `nil` であれば、条件式は `false` となり `if` ブロック内部のコードはスキップされます。  
値が `nil` ではない場合、オプショナル型の値はアンラップされ、`let` で宣言した定数(ここでは `name`)に格納されます。  
アンラップされた値( `let name` )は、`if` ブロック内部で使用することが出来ます。  

オプショナル型の値を扱う方法として、`??` 演算子を用いてデフォルト値を提供する方法もあります。  
もしオプショナル型の値が `nil` であれば、代わりにデフォルト値を使用します。

    let nickName: String? = nil
    let fullName: String = "John Appleseed"

    // nickNameがnilであれば、デフォルト値としてfullNameを使用する
    let informalGreeting = "Hi \(nickName ?? fullName)"

`switch` 構文は、あらゆる種類のデータと幅広い比較演算子をサポートします。  

    let vegetable = "red pepper"

    switch vegetable {
    case "celery":
        print("Add some raisins and make ants on a log.")
    case "cucumber", "watercress":
        print("That would make a good tea sandwich.")
    case let x where x.hasSuffix("pepper"):
        print("Is it a spicy \(x)?")
    default:
        print("Everything tastes good in soup.")
    }

条件がマッチするケースの処理が実行された後、プログラムは `switch` 文を終了します。  
次に記述されたケースの処理は実行されない為、明示的な `break` は必要ありません。

`key` と `value` のペアを用いて `Dictionary` のデータを反復する為には、`for-in` を用いることが出来ます。  
`Dictionary` は並び替えがされないコレクションなので、`key` と `value` は任意の順番で反復されます。

    // 辞書の宣言
    let interestingNumbers = [
        "Prime": [2, 3, 5, 7, 11, 13],
        "Fibonacci": [1, 1, 2, 3, 5, 8],
        "Square": [1, 4, 9, 16, 25],
    ]

    var largest = 0
    for (kind, numbers) in interestingNumbers {
        for number in numbers {
            if number > largest {
                largest = number
            }
        }
    }
    print(largest)

条件が変化するまでコードブロックを繰り返したい場合は、`while` を使用します。  
代わりに条件式を最後に置いて、処理が少なくとも1回は実行されるようにすることも可能です。

    // 条件式を前置した場合
    var n = 2
    while n < 100 {
        n *= 2
    }
    print(n)

    // 条件式を後置した場合
    var m = 2
    repeat {
        m *= 2
    } while m < 100
    print(m)

`..<` を用いることで、反復処理のインデックスを管理することが出来ます。

    var total = 0
    for i in 0..<4 {
        total += i
    }
    print(total)

右辺の値を含めない場合は `..<`、両方を含める場合は `...` を用いることが出来ます。

<!-- 改ページ -->
<div style="page-break-before:always"></div>

### <u>Functions and Closures(関数とクロージャ)</u>
関数を定義する為には、`func` を使用します。  
引数と戻り値を分割する為には、`->` を用います。

    func greet(person: String, day: String) -> String { // 戻り値はString
        return "Hello \(person), today is \(day)."
    }

    // 引数を入れるにはラベルが必要
    greet(person: "Bob", day: "Tuesday")

デフォルトでは、関数は引数のラベルとしてパラメータ名を使用します。  
パラメータ名の前に独自の引数ラベルを定義することも出来ますし、`_`を用いれば引数ラベルを使用しないことも可能です。

    func greet(_ person: String, on day: String) -> String {
        return "Hello \(person), today is \(day)."
    }
    
    // 引数1において、呼び出し時に引数ラベルを使用しない
    // 引数2において、呼び出し時に独自の引数ラベルを使用する
    greet("John", on: "Wednesday")

複合した値を作成するには `tuple` を用います。  
例えば、関数の戻り値として複数の値を返却することが出来ます。  
`tuple` の要素は名前とインデックスの両方で参照できます。

    // 戻り値は[min, max, sum]の3種類複合
    func calculateStatistics(scores: [Int]) -> (min: Int, max: Int, sum: Int) {
        var min = scores[0]
        var max = scores[0]
        var sum = 0
    
        for score in scores {
            if score > max {
                max = score
            } else if score < min {
                min = score
            }
            sum += score
        }
    
        return (min, max, sum)
    }

    let statistics = calculateStatistics(scores: [5, 3, 100, 3, 9])
    print(statistics.sum) // 名前での参照
    print(statistics.2)   // インデックスでの参照

関数はネストすることが出来ます。  
ネストされた関数では、その関数外に定義された値を参照することが可能です。  
ネスト関数は、コードが長くなってしまったり複雑になってしまっている関数を整理するのに役立ちます。

    func returnFifteen() -> Int {
        var y = 10

        // ネストされた関数
        func add() {
            // add()外に定義された値を参照可能
            y += 5
        }

        add()
        return y
    }
    returnFifteen()

Swiftにおいて関数は**第1級オブジェクト**です。  
これは、関数が別の関数を戻り値として返却できることを意味します。

    func makeIncrementer() -> ((Int) -> Int) {
        func addOne(number: Int) -> Int {
            return 1 + number
        }
        // 関数を戻り値として返却
        return addOne
    }
    var increment = makeIncrementer()
    increment(7)

別の関数を引数として取ることも可能です。

    func hasAnyMatches(list: [Int], condition: (Int) -> Bool) -> Bool {
        for item in list {
            // 条件式に引数で渡された関数を使用
            if condition(item) {
                return true
            }
        }
        return false
    }

    // 引数として渡す為の関数
    func lessThanTen(number: Int) -> Bool {
        return number < 10
    }

    var numbers = [20, 19, 7, 12]
    hasAnyMatches(list: numbers, condition: lessThanTen)

関数は実際、**クロージャ(無名関数)**の特殊なケースとして見ることが出来ます。  
クロージャとは、後で呼び出すことが可能なコードブロックの事です。(註：これだけでは何か分かりません)  
クロージャ内のコードは、たとえクロージャ実行時に別スコープにあったとしても、クロージャが作成された  
スコープにおいて使用可能な変数や関数にアクセスできます。(註：ここも何を言っているのか分かりづらいです)

クロージャは波括弧 `{ }` でコードを囲うことによって、無名関数として宣言できます。  
引数及び戻り値のブロックとコード本体を分ける為には、`in` を用います。

    numbers.map({ (number: Int) -> Int in
        let result = 3 * number
        return result
    })

クロージャをより簡潔に記述する為に、いくつかのオプションを使用することが出来ます。  
例えば、デリゲート時のコールバックのように、クロージャの型が既に判明している場合、  
引数と戻り値の両方の型を省略することは可能です。  

    // 引数と戻り値の型を省略し、1行で記述
    let mappedNumbers = numbers.map({ number in 3 * number })
    print(mappedNumbers)

名前の代わりにインデックスによってパラメータを参照することも出来ます。  
このアプローチは、非常に短いクロージャを記述する際に特に有用です。  
クロージャが関数の唯一の引数である場合は、波括弧 `{ }` も省略可能です。

    let sortedNumbers = numbers.sorted { $0 > $1 }
    print(sortedNumbers)

<!-- 改ページ -->
<div style="page-break-before:always"></div>

### <u>Objects and Classes(オブジェクトとクラス)</u>
**クラス**は、`class` のあとにクラス名を宣言することで作成できます。  
クラス内の変数宣言は、`let` や `var` と同様の方法で宣言することが可能です。

    class Shape {
        // クラス変数の宣言
        var numberOfSides = 0

        // 関数の宣言
        func simpleDescription() -> String {
            return "A shape with \(numberOfSides) sides."
        }
    }

クラスのインスタンスを作成するには、`クラス名()` と記述します。  
インスタンスのプロパティやメソッドにアクセスするには、`インスタンス.プロパティ名` や  
`インスタンス.メソッド名()` のように記述します。

    // インスタンスの生成
    var shape = Shape()

    // プロパティの参照、値の代入
    shape.numberOfSides = 7

    // メソッドの呼び出し
    var shapeDescription = shape.simpleDescription()

この `Shape` クラスには重要なものが欠けています。  
インスタンスが生成された際にクラスをセットアップする<u>**イニシャライザ**</u>がありません。  
イニシャライザを作成するには、`init` を用います。

    class NamedShape {
        var numberOfSides: Int = 0
        var name: String

        // initializer
        init(name: String) {
            self.name = name
        }

        func simpleDescription() -> String {
            return "A shape with \(numberOfSides) sides."
        }
    }

イニシャライザの `name` 引数と、クラスが持つ `name` プロパティを区別するために、  
`self` キーワードが使用されていることに注目してください。  
イニシャライザの引数は、クラスのインスタンス作成時に関数呼び出しのような形で渡されます。  
全てのプロパティは、`numberOfSides` のように定義時か、`name` のようにイニシャライザによって  
必ず値が割り当てられなければなりません。  

オブジェクトの解放前に何かしらのクリーンアップを行いたい場合は、  
`deinit` を用いて `deinitializer` を作成します。  

サブクラスは、クラス名の後ろにコロン区切りで親クラスの名前を定義します。  
クラスが標準のルートクラスをサブクラス化する必要はないので、必要に応じてスーパークラスを  
インクルードしたり省略したりすることができます。

サブクラスで親クラスのメソッドをオーバーライドする場合、`override` を付与します。  
もし不意に、 `override` キーワード無しで親クラスの実装をオーバーライドしてしまった場合、  
コンパイラがエラーと判断します。  
親クラスに実装が無いメソッドに対して `override` キーワードが付与された場合も同様に  
エラーと判断されます。

    class Square: NamedShape {
        var sideLength: Double

        // initializer
        init(sideLength: Double, name: String) {
            self.sideLength  sideLength
            super.init(name: name)
            numberOfSides = 4
        }

        func area() -> Double {
            return sideLength * sideLength
        }

        override func simpleDescription() -> String {
            return "A square width sides of length \(sideLength)."
        }
    }

    // initializerを用いたインスタンス化
    let test = Square(sideLength: 5.2, name: "my test square")

    // メソッドの呼び出し
    test.area()
    test.simpleDescription()

単純なプロパティに加えて、プロパティには `getter` と `setter` が存在します。

    class EquilateralTriangle: NamedShape {
        var sideLength: Double = 0.0

        // initializer
        init(sideLength: Double, name: String) {
            self.sideLength = sideLength
            super.init(name: name)
            numberOfSides = 3
        }

        // 周囲長パラメータ
        var perimater: Double {
            // getter
            get {
                return 3.0 * sideLength
            }

            // setter
            set {
                sideLength = newValue / 3.0
            }
        }

        override func simpleDescription() -> String {
            return "An equilateral triangle with sides of length \(sideLength)."
        }
    }

    // initializerを用いたインスタンス化
    var triangle = EquilateralTriangle(sideLength: 3.1, name: "a triangle")

    // getter呼び出し
    print(triangle.perimeter)
    // setter呼び出し
    triangle.perimeter = 9.9

    // パラメータ呼び出し
    print(triangle.sideLength)

周囲長パラメータの `setter` では、新規の値は暗黙的に `newValue` となります。  
値のセット後、括弧の中で明示的な名称を付けることが可能です。  

`EquilateralTriangle` クラスのイニシャライザには、次の3つのステップが有ります。  

1. サブクラスに定義されたプロパティへの値のセット。
1. 親クラスのイニシャライザの呼び出し。
1. 親クラスによって定義されたプロパティの値変更。  
   メソッド、ゲッター、セッターを使用した追加セットアップはここで実行可能。

「プロパティの演算は必要ないが、新規の値を設定する前後に実行されるコードを記述したい」  
といった場合には、`willSet` や `didSet` を使用します。  
`willSet` や `didSet` に記述されたコードは、イニシャライザの外部で値が変更されるたびに実行されます。  
例えば以下のクラスでは、三角形の辺の長さが常に四角形の辺の長さと同じであることを保証しています。

    class TriangleAndSquare {
        var triangle: EquilateralTriangle {
            willSet {
                square.sideLength = newValue.sideLength
            }
        }

        var square: Square {
            willSet {
                triangle.sideLength = newValue.sideLength
            }
        }

        // initializer
        init(size: Double, name: String) {
            square = Square(sideLength: size, name: name)
            triangle = EquilateralTrinangle(sideLength: size, name: name)
        }
    }

    // initializerを用いたインスタンス化
    var triangleAndSquare = TriangleAndSquare(size: 10, name: "another test shape")

    print(triangleAndSquare.square.sideLength)
    print(triangleAndSquare.triangle.sideLength)

    triangleAndSquare.square = Square(sideLength: 50, name: "larger square)
    print(triangleAndSquare.triangle.sideLength)

オプショナル型として実行したい場合は、  
メソッド、プロパティ、サブスクリプトといったオペレーションの前に `?` を付けることが出来ます。  
`?` の前にある値が `nil` だった場合、`?` 以降の処理は全て無視され、値全体が `nil` として評価されます。  
値が存在した場合、オプショナル型はアンラップされ、`?` 以降はアンラップされた値として動作します。  
以下どちらのケースでも、式全体の値はオプショナル型です。

    let optionalSquare: Square? = Square(sideLength: 2.5, name: "optional square")
    let sideLength = optionalSquare?.sideLength

<!-- 改ページ -->
<div style="page-break-before:always"></div>

### <u>Enumerations and Structures(列挙型と構造体)</u>
列挙型を作成するには `enum` を用います。  
クラス等と同様に、列挙型はそれに関連するメソッドを保持することが可能です。

    enum Rank: Int {
        // 列挙子の宣言
        case ace = 1
        case two, three, four, five, six, seven, eight, nine, ten
        case jack, queen, king

        func simpleDescription() -> String {
            switch self {
                case .ace:
                    return "ace"
                case .jack:
                    return "jack
                case .queen:
                    return "queen"
                case .king:
                    return "king"
                default:
                    return String(self.rawValue)
            }
        }
    }

    let ace = Rank.ace
    let aceRawValue = ace.rawValue

デフォルトでは、Swiftは0から始まって1ずつインクリメントする `raw values` をアサインしますが、  
明示的に値を指定することで動作を変更することが出来ます。  
上記の例では、`Ace` は `1` という `raw value` を与えられており、残りの `raw value` は順番に  
アサインされています。  
列挙型の `raw type` には、`String` や `Float` 等を用いることも可能です。  

`raw value` から列挙型のインスタンスを作成するには、`init?(rawValue:)` イニシャライザを使用します。  
このイニシャライザは、指定した `raw value` にマッチするケースか、もしくは `nil` を返却します。

    // Optional Binding
    if let convertedRank = Rank(rawValue: 3) {
        let threeDescription = convertedRank.simpleDescription()
    }

列挙型におけるケースの値は実際の値であり、`raw value` を記述する為の別の方法というわけではありません。  
実際、ケース自体に意味のある `raw value` が無い場合は、`raw value` を記述する必要はありません。

    enum Suit {
        // 列挙子の宣言
        case spades, hearts, diamonds, clubs

        func simpleDescription() -> String {
            switch self {
                case .spades:
                    return "spades"
                case .hearts:
                    return "hearts"
                case .diamonds:
                    return "diamonds"
                case .clubs:
                    return "clubs"
            }
        }
    }

    let hearts = Suit.hearts
    let heartsDescription = hearts.simpleDescription()

上記の例で、列挙型の `hearts` ケースへの参照方法が2種類あることに注目してください。  
`hearts` 定数に値を割り当てる時には、定数自体に明示的な型指定が無いため、  
列挙型 `Suit.hearts` はフルネームで参照されます。  

一方、`switch` 構文の内部では省略形 `.hearts` によって参照されています。  
これは `self` の値が既に `Suit` であることが分かっている為です。  

このように、値の型が既に分かっている場合は、いつでも省略形を使用することが可能です。  

列挙型が `raw values` を保持している場合、それらの値は宣言の一部と見なされます。  
つまり、特定の列挙型から生成されるインスタンスは全て同じ `raw values` を持つことになります。  

列挙型のケースにおける別の選択肢として、ケースに関連した値を持つということが挙げられます。  
それらの値はインスタンス生成時に決定され、各インスタンス毎に異なる値を持つことが出来ます。

関連付けられた値というのは、列挙型のインスタンス内に格納されたプロパティのように振る舞うと  
考えることが出来ます。  

例えば、サーバーから日の出と日没の時間を要求する場合を考えてみましょう。  
サーバーは、要求された情報を応答するか、もしくはエラーの説明を応答します。

    enum ServerResponse {
        case result(String, String)
        case failure(String)
    }

    let success = ServerResponse.result("6:00 am", "8:09 pm")
    let failure = ServerResponse.failure("Out of cheese.")

    switch success {
        case let .result(sunrise, sunset):
            print("Sunrise is at \(sunrise) and sunset is at \(sunset).")
        case let .failure(message):
            print("Failure... \(message)")
    }

ここでは `switch` のケースと実際の値をマッチさせる際に、`ServerResponse` の値から日の出と日没の時間が  
一体どのように抽出されているか、という点に注目してください。  

構造体を作成するには、`struct` を使用します。構造体は、メソッドやイニシャライザを含む、クラスと同等の  
振る舞いを多数サポートしています。  
構造体とクラスの重要な違いの一つに、値の受け渡しがあります。  
構造体は値渡し(値のコピーを渡す)ですが、クラスは参照渡しです。

    struct Card {
        var rank: Rank
        var suit: Suit
        func simpleDescription() -> String {
            return "The \(rank.simpleDescription()) of \(suit.simpleDescription())"
        }
    }

    let threeOfSpades = Card(rank: .three, suit: .spades)
    let threeOfSpadesDescription = threeOfSpades.simpleDescription()

<!-- 改ページ -->
<div style="page-break-before:always"></div>

### <u>Protocols and Extensions(プロトコルとエクステンション)</u>
プロトコルを宣言するには、`protocol` を使用します。
(他言語で言うところのinterfaceに当たります。)

    // プロトコルの宣言
    protocol ExampleProtocol {
        var simpleDescription: String { get }
        mutating func adjust()
    }

クラス、列挙型、構造体のすべてがプロトコルを使うことが出来ます。

    // クラスの場合
    class SimpleClass: ExampleProtocol {
        var simpleDescription: String = "A very simple class."
        var anotherProperty: Int = 69105
        func adjust() {
            simpleDescription += " Now 100% adjusted."
        }
    }
    var a = SimpleClass()
    a.adjust()
    let aDescription = a.simpleDescription

    // 構造体の場合
    struct SimpleStructure: ExampleProtocol {
        var simpleDescription: String = "A simple structure"
        mutating func adjust() {
            simpleDescription += " (adjusted)"
        }
    }
    var b = SimpleStructure()
    b.adjust()
    let bDescription = b.simpleDescription

ここでは、`SimpleStructure` 内で構造体を修正するようなメソッドに対して、  
`mutating` キーワードを用いてマークするということに注意してください。  

構造体と比べて、`SimpleClass` 内のメソッドはクラスをいつでも修正することが出来るため、  
`mutating` キーワードを用いてメソッドをマークする必要はありません。  

既に存在する型に対して、新規メソッドの追加やプロパティの演算等の機能を追加したい場合は、  
`extension` を使用します。`extension` を用いることで、他の場所で定義されている型はもちろん、  
ライブラリやフレームワークからインポートした型にさえも、プロトコルを適合させることが出来ます。

    extension Int: ExampleProtocol {
        var simpleDescription: String {
            return "The number \(self)"
        }

        mutating func adjust() {
            self += 42
        }
    }

    print(7.simpleDescription)

プロトコル名は、他の名称付きの型と同じように使うことが出来ます。例えば、異なる型のコレクションですが、  
一つのプロトコルに準拠するコレクションを作成するといったことが可能です。  
値の型指定がプロトコルである場合は、プロトコルに定義されたメソッド以外は使用できません。

    let protocolValue: ExampleProtocol = a
    print(protocolValue.simpleDescription)
    // print(protocolValue.anotherProperty) // プロトコル外に定義されている為エラー

変数 `protocolValue` が実行時の型として `SimpleClass` を持っていたとしても、  
コンパイラは `ExampleProtocol` 型として扱います。  
このことは、プロトコルの適合性を示すとともに、クラスの実装(メソッドやプロパティ)に対する  
誤ったアクセスが不可能なことを示しています。

<!-- 改ページ -->
<div style="page-break-before:always"></div>

### <u>Error Handling(エラーハンドリング)</u>
`Error` プロトコルに準拠するあらゆる型を使用してエラーを表すことが可能です。

    enum PrinterError: Error {
        case outOfPaper
        case noToner
        case onFire
    }

`throw` を使用することで、エラーをスローすることが出来ます。また、`throws` を使用してエラーを  
スロー可能なメソッドをマークすることが出来ます。  
関数内でエラーをスローした場合、関数は即座にリターンし、その関数を呼び出したコードが  
エラーを処理します。

    func send(job: Int, toPrinter printerName: String) throws -> String {
        if printerName == "Never Has Toner" {
            throw PrinterError.noToner
        }
        return "Job sent"
    }

エラーを操作するにはいくつかのやり方が存在します。ひとつは `do-catch` を用いる方法です。  
`do` ブロックでは、エラーをスロー可能なコードの前に `try` を付与して、そのコードをマークします。  
`catch` ブロックではエラーに対し、異なる名称を与えない限りは、即座に `error` という名前が与えられます。  

    do {
        let printerResponse = try send(job: 1040, toPrinter: "Bi Sheng")
        print(printerResponse)
    } catch {
        print(error)
    }

特定のエラーを操作する為に、複数の `catch` ブロックを記述することが出来ます。  
`switch` のケースの記述と同じように、`catch` の後に別の `catch` を記述します。

    do {
        let printerResponse = try send(job: 1040, toPrinter: "Gutenberg")
        print(printerResponse)
    } catch PrinterError.onFire {
        print("I'll just put this over here, with the rest of the fire.")
    } catch let printerError as PrinterError {
        print("Printer error: \(printerError).")
    } catch {
        print(error)
    }

エラーを操作する別の方法として、`try?` を用いて結果をオプショナル型に変換する方法があります。  
関数がエラーをスローした場合、エラーの内容は破棄され、返り血として `nil` が返却されます。  
エラーがスローされなければ、関数の戻り値を含むオプショナル型の値が結果として返却されます。

    let printerSuccess = try? send(job: 1884, toPrinter: "Mergenthaler")
    let printerFailure = try? send(job: 1885, toPrinter: "Never Has Toner")

関数内の全てのコードが実行された後に動かしたいコードブロックを記述する際は `defer` を使用します。  
`defer` によって定義されたコードブロックは、**エラーがスローされたかどうかに関わらず実行されます。**  
`defer` キーワードはセットアップやクリーンアップのコードを記述する際に使用することが出来ます。  
たとえそれらの実行タイミングが別々であっても、隣同士に書くことが可能です。

    var fridgeIsOpen = false
    let fridgeContent = ["milk", "eggs", "leftovers"]

    func fridgeContains(_ food: String) -> Bool {
        fridgeIsOpen = true

        // 冷蔵庫は使い終わったら最後に必ず閉めますよね？
        defer {
            fridgeIsOpen = false
        }

        let result = fridgeContent.contains(food)
        return result
    }

    fridgeContains("banana")
    print(fridgeIsOpen) // false

<!-- 改ページ -->
<div style="page-break-before:always"></div>

### <u>Generics(ジェネリクス)</u>
ジェネリクス関数の型を指定するには、カギ括弧 `< >` の中に名称を記述します。

    func makrArray<Item>(repeating item: Item, numberOfTimes: Int) -> [Item] {
        var result = [Item]()

        for _ in 0..<numberOfTimes {
            result.append(item)
        }

        return result
    }

    makeArray(repeating: "knock", numberOfTimes: 4)

関数、メソッド、クラス、列挙型、構造体などの汎用的な形式を作成することも可能です。

    enum OptionalValue<Wrapped> {
        case none
        case some(Wrapped)
    }

    var possibleInteger: OptionalValue<Integer> = .none
    possibleInteger = .some(100)

`where` キーワードを使用することで、関数本体の直前部分に必須条件の指定を記述することが出来ます。  
例えば、特定のプロトコルの実装を要求したり、2つの型が同じであることを要求したり、特定の親クラスを持つ  
ことを要求したり出来ます。

    func anyCommonElements<T: Sequence, U: Sequence>(_ lhs: T, _ rhs: U) -> Bool
        where T.Iterator.Element: Equatable, T.Iterator.Element == U.Iterator.Element {
            for lhsItem in lhs {
                for rhsItem in rhs {
                    if lhsItem == rhsItem {
                        return true
                    }
                }
            }

            return false
        }
    }

    anyCommonElements([1, 2, 3], [3])

`<T: Equatable>` という記法は、`<T>...where T :Equatable` という記法と同じです。