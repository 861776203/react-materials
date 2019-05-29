---
title: Linkage Show/Hide
order: 5
---

联动 status="show" 或者 status="hide"

````jsx
import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import { Form, Field } from '@ice/form';

const sleep = ms => new Promise(resolve => setTimeout(resolve, ms))

class App extends Component {
  async onSubmit(values) {
    await sleep(300)
    window.alert(JSON.stringify(values, 0, 2))
  }

  render() {
    return (
      <div>
        <Form
          onSubmit={this.onSubmit}
          style={{color: '#ee7893'}}
          rules={{
            username: [{
              required: true,
              min: 5,
              message: '姓名至少5个字符'
            }]
          }}
        >
          <div>Hello Form</div>
          <Field label="姓名：" name="username" component="input" type="text" />
          <Field label="昵称：" name="nickname" component="input" type="text" linkages={{
            handler: formCore => {
              if (formCore.getValue('nickname') === 'snow') {
                formCore.setStatus('age', 'show');
              } else {
                formCore.setStatus('age', 'hide');
              }
            }
          }} />
          <Field label="年龄：" name="age" component='input' type="number" status="hide" rules={[{
            required: true,
            message: '年龄必填'
          }]} />
          <button type="submit">Submit</button>
        </Form>
      </div>
    );
  }
}

ReactDOM.render((
  <App />
), mountNode);
````