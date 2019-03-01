<template>
<div class="loggin">
    <van-nav-bar
        title="登录"
        left-text="返回"
        @click-left="back"
        />
    <div class="entry">
    <van-field
            v-model="sms"
            center
            clearable
            placeholder="请输入手机号码"
            @focus="entry"
            @blur="cancle"
        >
        <van-button slot="button" size="small" :disabled="ty" type="primary" @click="send">{{msg}}</van-button>
    </van-field>
    <van-cell-group>
        <van-field  placeholder="请输入验证码"  />
    </van-cell-group>
    <div class="context">
        <van-checkbox v-model="checked" checked-color="#ff4891">我已阅读理解并同意《每日优鲜用户协议》</van-checkbox>
    </div>
    <button class="submit">确认</button>
    </div>
    <van-number-keyboard
        :show="show"
        extra-key="."
        close-button-text="完成"
        @blur="show = false"
        @input="onInput"
        @delete="onDelete"
    />
</div>
</template>

<script>
import { Notify } from 'vant';
export default {
    name:'Loggin',
    data(){
        return {
            sms:'',
            msg:'发送验证码',
            ty:false,
            show:false,
            radio:true,
            checked:true
        }
    },
    methods:{
        send(){
            // console.log(1)
            this.msg="已发送"
            this.ty = true;
            Notify({
                message: '验证码为2333',
                duration: 2000,
                background: '#ff4891'
            });
        },
        entry(){
            this.show = true
        },
        cancle(){
            this.show = false
        },
        onInput(key) {
            this.sms = (this.sms + key).slice(0, 11);
        },
        onDelete() {
            this.sms = this.sms.slice(0, this.sms.length - 1);
        },
        back(){
            this.$router.back()
        }
    }
}
</script>

<style scoped>
.loggin{
    width: 100%;
    padding: 0px 15px 0px 15px ;
    box-sizing: border-box
}
.entry{
    padding-top: 20px;
    box-sizing: border-box
}
.procotol{
    color: #ff4891;
    text-decoration: underline
}
.van-field__control{
    margin-bottom: 20px;
}
.context{
    padding: 30px 0px;
    text-align: left;
    vertical-align: center;
}
.submit{
    width: 300px;
    height: 40px;
    border: none;
    background: #ff4891;
    color: #fff;
    font-size: 20px;
    border-radius: 10px;
}
</style>

