<template>
    <div class="center">
        <div id="b1" class="sub-box">
            <div class="box-top">
                <div class="prop-name">{{ prop_name }}</div>
                <div class="star-line">
                    <div v-for="count in star_number" :key=count class="star">

                    </div>
                </div>

                <div class="info">
                    <div style="color: white;text-align: center;margin-top: 3px;">
                        当前持有:{{ amount }}
                    </div>
                </div>
                <div class="coin-line">
                    <div class="coin">
                    </div>
                    {{ coin_number }}
                </div>
            </div>
            <div class="box-bottom">
                <div class="description">
                    {{ description }}
                </div>
                <div class="line" style="height: 2px;background-color: #d7d7d7;">

                </div>
                <div class="remark">
                    {{ remark }}
                </div>
                <button class="button" @click="handleButtonClick">
                    兑换
                </button>
            </div>
        </div>
    </div>
</template>
<script>
import { defineComponent, toRefs } from 'vue';
export default defineComponent({
    name: 'StoreCardPlus',
    /*
prop_name 道具名
amount:当前持有数量
star_number 星星数量
coin_number 金币数量
description 第一段描述
remark 第二段补充文字
onButtonClick 兑换按钮传入函数
*/
    props: {
        prop_name: String,
        amount: Number,
        star_number: {
            type: Number
        },
        coin_number: Number,
        description: String,
        remark: String,
        // 用来接收父组件传递的点击事件处理方法
        onButtonClick: {
            type: Function,
            required: true, // 确保父组件传入这个方法
        }
    },
    setup(props) {
        // 使用 toRefs 将 props 转化为响应式对象
        const { onButtonClick } = toRefs(props);

        // 定义点击按钮时触发的方法
        const handleButtonClick = () => {
            if (onButtonClick.value) {
                onButtonClick.value(); // 调用父组件传入的回调方法
            }
        };

        return {
            handleButtonClick
        };
    }
});
</script>
<style scoped>
.center {
    /* 将盒子偏移自身宽高的一半 */
    display: flex;
    justify-content: center;
}

.sub-box {
    width: 270px;
    height: 430px;
    margin: 10px;
    background-color: #e4e4e4;
}

.box-top {
    height: 160px;
    width: 100%;
    background: linear-gradient(to bottom left, #424e75, #7489bd);
    position: relative;
    /* 设置定位，让子元素参照 */
}

.prop-name {
    color: white;
    padding-top: 10px;
    padding-left: 20px;
    text-shadow: 2px 2px 2px #000000;

}

.star-line {
    display: flex;
    /* 使用 Flexbox */
    flex-wrap: wrap;
    /* 允许换行 */
    padding-left: 18px;

}

.star {
    width: 15px;
    height: 15px;
    margin-top: 8px;
    margin-left: 2px;
    background-image: url('../assets/image/star-color.png');
    /* 五角星图片路径 */
    background-size: cover;

}

.info {
    background-color: #242e46;
    position: absolute;
    /* 绝对定位 */
    bottom: 28px;
    /* 离底部为 0 */
    width: 100%;
    height: 28px;
}

.coin-line {
    background-color: #c3cada;
    position: absolute;
    /* 绝对定位 */
    bottom: 0;
    /* 离底部为 0 */
    width: 100%;
    height: 28px;
    display: flex;
    justify-content: center;
    align-items: center;
}

.coin {
    width: 15px;
    height: 15px;
    margin-top: 8px;
    background-image: url('../assets/image/coin-color.png');
    /* 五角星图片路径 */
    background-size: cover;
    margin-bottom: 7px;
    margin-right: 3px;
}

.box-bottom {
    padding: 8px;
    position: relative;
    /* 设置定位，让子元素参照 */
    height: 270px;
}

.description {
    font-size: 14px;
    margin-bottom: 15px;
}

.remark {
    font-size: 12px;
    color: #959595;
    margin-top: 15px;
}

.button {
    position: absolute;
    bottom: 10%;
    width: 95%;
    height: 33px;
    border-radius: 15px;
    /* 设置圆角半径 */
    background-color: #fefefe;
    display: flex;
    justify-content: center;
    align-items: center;
    border: none;
}

#b2 {
    background-color: green;
    /* 绿色 */
}

#b3 {
    background-color: blue;
    /* 蓝色 */
}
</style>