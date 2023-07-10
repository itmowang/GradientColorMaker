<!-- 仿colors头部导航 -->
<template>
    <div class="header">
        <!-- logo -->
        <div class="header-left">
            <img class="header-left-logo" src="../assets/logo.svg" alt="">
        </div>
        <div class="header-right">
            <div class="header-right-li">
                <div>Tools</div>
                <div>Jobs</div>
                <div class="active">GoPro</div>
                <div class="after"></div>
            </div>
            <div class="header-right-Login">
                <div>Sign in </div>
                <div class="login-btn">Sign up</div>
            </div>
        </div>
    </div>
</template>
<script setup>
 
</script>
<style lang="less">
.header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 20px;
    height: 60px;
    border-bottom: 1px solid #e6e6e6;
    .header-left {
        display: flex;
        align-items: center;
        .header-left-logo {
            width: 100px;
            height: 50px;
        }
    }
    .header-right {
        display: flex;
        align-items: center;
        .header-right-li {
            display: flex;
            align-items: center;
            font-weight: 600;
            .active{
                color: #FF0096;
            } 
            .after{
                width: 1px;
                height: 20px;
                background-color: #e6e6e6;
                margin: 0 10px;
            }   
            div {
                margin: 0 10px;
                font-size: 14px;
                color: #333;
                cursor: pointer;
            }
        }
        .header-right-Login {
            display: flex;
            align-items: center;
            font-weight: 600;
            div {
                margin: 0 10px;
                font-size: 14px;
                color: #333;
                cursor: pointer;
            }
            .login-btn{
                width: 80px;
                height: 30px;
                padding: 2px 0;
                background-color: #0066ff;
                color: #fff;
                display: flex;
                justify-content: center;
                align-items: center;
                border-radius: 5px;
                cursor: pointer;
            }
        }
        
    }
}
</style>