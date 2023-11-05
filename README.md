# JS-Assignment
 UI library using Snabbdom and Lerna, and then use this library to build a simple web page with the specified elements. 
// ui-library.js
import snabbdom from 'snabbdom';

const { h, patch } = snabbdom.init([]);

class UIComponent {
  constructor() {
    this.state = {
      count: 0,
    };
  }

  updateState(newState) {
    this.state = { ...this.state, ...newState };
    this.render();
  }

  render() {
    const vnode = this.template();
    patch(this.vnode, vnode);
    this.vnode = vnode;
  }

  mount(element) {
    this.element = element;
    this.vnode = this.template();
    patch(element, this.vnode);
    this.componentDidMount();
  }

  componentDidMount() {
    console.log('Component mounted.');
  }

  template() {
    return h('div', {}, [
      h('h1', `Count: ${this.state.count}`),
      h('button', { on: { click: this.handleClick.bind(this) } }, 'Add'),
    ]);
  }

  handleClick() {
    this.updateState({ count: this.state.count + 1 });
    console.log('State updated.');
  }
}

export function createUIComponent() {
  return new UIComponent();
}
