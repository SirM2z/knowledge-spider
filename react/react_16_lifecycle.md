1. 创建阶段 `Mounting`
    1. `constructor()` 
        - 初始化 `state`
        - 函数绑定 `this`
        - `ES6` 子类的构造函数必须执行一次 `super()`
        - `React` 如果构造函数中要使用 `this.props`，必须先执行 `super(props)`
    2. `static getDerivedStateFromProps(nextProps, prevState)`
        - 静态方法，不会被实例继承，即调用类的方法本身
        - 当创建时、接收新的 `props` 时、 `setState` 时、 `forceUpdate` 时会执行这个方法
        - `nextProps` 是新接收的 `props` ，`prevState` 是当前的 `state`
        - 返回值（对象）将用于更新 `state`，如果不需要更新则需要返回 `null`
        - 建议少用，对标 `componentWillReceiveProps`
    3. `componentWillMount()`/`UNSAFE_componentWillMount()`（弃用）
        - 可以使用 `setState`，不会触发 `re-render`
    4. `render()`
        - 必须有，可以返回 `React elements`,`Arrays`（v16.0.0 新增）,片段（`fragments`）v16.2.0 新增,插槽（`Portals`）V16.0.0 新增, `String or numbers or Booleans or null`
        - 不能使用 `setState`
    5. `componentDidMount()`
        - 组件完成装载（已经插入 `DOM` 树）时，触发该方法
        - 用于 异步请求 `ajax`、添加事件绑定
        - 可以使用 `setState`，触发 `re-render`，影响性能
2. 更新阶段 `Updating`
    1. `componentWillReceiveProps()`/`UNSAFE_componentWillReceiveProps()`（弃用）
        - 接收新的 `props` 时触发，即使没有变化
        - 可以使用 `setState`
    2. `static getDerivedStateFromProps()` 同上
    3. `shouldComponentUpdate()`
        - 在接收新的 `props` 或新的 `state` 时，在渲染前会触发该方法
        - 返回 `true` 或 `false` 来确定是否需要触发新的渲染
    4. `componentWillUpdate()`/`UNSAFE_componentWillUpdate()` （弃用）
        - 当接收到新的 `props` 或 `state` 时，在渲染前执行该方法
        - 不能使用 `setState`
    5. `render()` 同上
    6. `getSnapshotBeforeUpdate(prevProps, prevState)`
        - 这个方法在 `render()` 之后，`componentDidUpdate()` 之前调用
        - 参数 `prevProps` 表示更新前的 `props`，`prevState` 表示更新前的 `state`
        - 返回值称为一个快照（`snapshot`），如果不需要 `snapshot`，则必须显示的返回 `null`
        - 返回值将作为 `componentDidUpdate()` 的第三个参数使用。这个函数必须要配合 `componentDidUpdate()` 一起使用
        - 这个函数的作用是在真实 `DOM` 更新（`componentDidUpdate`）前，获取一些需要的信息（类似快照功能），然后作为参数传给 `componentDidUpdate`。例如：在 `getSnapShotBeforeUpdate` 中获取滚动位置，然后作为参数传给 `componentDidUpdate`，就可以直接在渲染真实的 `DOM` 时就滚动到需要的位置
    7. `componentDidUpdate(prevProps, prevState, snapshot)`
        - 更新完成之后调用
        - 可以使用 `setState`，会触发 `re-render`，所以要注意判断，避免导致死循环
3. 卸载阶段 `Unmounting`
    1. `componentWillUnmount()`
        - 取消定时器/取消事件绑定/取消网络请求
        - 不能使用 setState
4. 错误处理 `Error Handling`
    1. `componentDidCatch()`
        - 任何子组件在渲染期间，生命周期方法中或者构造函数 `constructor` 发生错误时调用

### 注意

1. 有定义 `getDerivedStateFromProps` 时，会忽略 `componentWillMount()`/`UNSAFE_componentWillMount()`/`componentWillReceiveProps()`/`UNSAFE_componentWillReceiveProps()`