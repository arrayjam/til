I have a React component that renders a chart with d3, which uses `this.refs.svg.getBoundingClientRect().width` for scale computations. In order to make React re-render this chart, we can wrap it in a `<Resizable>` component like this:

```
export const Resizeable = React.createClass({
  propTypes: {
    children: React.PropTypes.element.isRequired,
  },

  getInitialState() {
    return { width: null };
  },

  componentDidMount() {
    window.addEventListener("resize", this.handleResize);
  },

  componentWillUnmount() {
    window.removeEventListener("resize", this.handleResize);
  },

  handleResize() {
    const newWidth = this.refs.child.clientWidth;
    if (this.state.width !== newWidth) {
      this.setState({ width: newWidth });
    }
  },

  render() {
    return (
      <div ref="child" key={this.state.width}>{ this.props.children }</div>
    );
  },
});

ReactDOM.render(<Resizeable><Chart></Resizeable>, container);
```

This wrapper component keeps track of its current width, and if it changes, uses that as a rendering key.

If the page gets resized, but the component remains the same width (i.e. the page uses fixed breakpoints) the child components will not get re-rendered. If the page gets resized and the component width changes, then the rendering key will change, which will prompt React to actually re-render the component.