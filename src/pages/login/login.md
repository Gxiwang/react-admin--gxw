import React, {Component} from 'react'
import {Form, Input, Button, Icon} from 'antd'
import Logo from './../../assets/images/logo.png'
import './index.less'

// import Item from "antd/lib/list/Item.d";
const Item = Form.Item


export default class Login extends Component {
  render() {
    return (
      <div className='login'>
        <div className="login-header">
          <img src={Logo}/>
          React项目: 后台管理系统
        </div>
        <div className="login-content">
            <div className='login-box'>
                <div className="title">用户登陆</div>
                <LoginForm/>
            </div>
        </div>
      </div>
    )
  }
}
class LoginForm extends React.Component{
    clickLogin = () =>{
        this.props.form.validateFields((error,values)=>{
            if(!error){
                console.log(error)
                console.log('收集表单数据',values)
                this.props.form.resetFields()
            }else{
                alert('错误的登录')
            }
        })
    }
    checkPassword = (rule,value,callback) =>{
        if(!value){
            callback('必须输入密码')
        }else if(value.length<4 || value.length>8){
            callback('密码不能小于4位或大于8位')
        }else{
            callback()
        }
    }
    render(){
        const {getFieldDecorator} =this.props.form

        return(
            <Form className='login-form'>
                <Item>
                   {
                       getFieldDecorator('userName',{
                           initialValue: 'admin',
                           rules:
                               [{required:true,message:'必须输入用户名'},
                                {min:4,message:'用户名不得小于4'}]
                       })(
                           <Input placeholder='请输入用户名' prefix={<Icon type="user"/> }/>
                       )
                   }
                </Item>
                <Item>
                    {
                        getFieldDecorator('password',{
                            rules:[{validator: this.checkPassword}]
                        })(
                            <Input type='password' placeholder="请输入密码" prefix={<Icon type="lock"/>}/>
                        )
                    }
                </Item>
                <Item>
                    <button type="primary" className='login-form-button' onClick={this.clickLogin}>登录</button>
                </Item>

            </Form>
        )

    }
}
LoginForm = Form.create()(LoginForm)