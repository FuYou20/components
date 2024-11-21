<template>
    <div :class="cardStyleClass">
        <div class="card">
            <div :class="statusClass" style="font-size: 10px;">
                {{ state }}:{{ state_text }}
            </div>
            <div class="info">
                <div style="color: white;text-align: center;margin-top: 3px;font-size: 13px;">
                    {{ prop_name }}
                </div>

            </div>
            <div class="star-line">
                <div v-for="count in star_number" :key=count class="star"></div>
            </div>
            <div class="coin-line">
                <div class="coin">
                </div>
                <div :class="coinNumberClass">
                    {{ coin_number }}
                </div>
            </div>
        </div>
    </div>

</template>

<script>
import { computed, defineComponent } from 'vue';
export default defineComponent({
    /*
prop_name 道具名
star_number 星星数量
coin_number 金币数量
state 道具状态（商店：可兑换|已售空）
state_text 状态文字
afford 金币是否充足
*/
    props: {
        prop_name: String,
        star_number: Number,
        coin_number: Number,
        state: String,
        state_text: String,
        afford: Boolean
    },
    setup(props) {
        const { state, afford } = props
        /*左上角提示标签样式*/
        const statusClass = computed(() => {
            if (state === '可兑换' || state === '金币不够') {
                return 'state-available';  // 可兑换状态，黄色
            } else if (state === '已售空') {
                return 'state-sold-out';  // 已售空状态，灰色
            }
            return '';
        });
        /*整个道具卡片样式（动态加遮罩层）*/
        const cardStyleClass = computed(() => {
            if (state === '已售空') {
                return 'state-card-disable';
            }
            return ''
        });
        /*金币数量样式动态渲染*/
        const coinNumberClass = computed(() => {
            if (afford === false) {
                return 'coin-shortage';
            }
            return ''
        })
        return {
            statusClass,
            cardStyleClass,
            coinNumberClass
        }

    }
})

</script>
<style scoped>
.card {
    height: 155px;
    width: 120px;
    background: linear-gradient(to bottom left, #424e75, #7489bd);
    position: relative;
    /* 使用绝对定位 */
    /* 设置定位，让子元素参照 */
}

.info {
    position: absolute;
    /* 绝对定位 */
    bottom: 40px;
    /* 离底部为 0 */
    width: 100%;
    height: 28px;
}

.star-line {
    position: absolute;
    display: flex;
    /* 使用 Flexbox */
    flex-wrap: wrap;
    /* 允许换行 */
    padding-left: 18px;
    bottom: 29px;
}

.star {
    width: 15px;
    height: 15px;
    margin-top: 8px;
    margin-left: 2px;
    background-image: url('../assets/image/star-color.png');
    /*五角星图片路径 */
    background-size: cover;
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
    /* 金币图片路径 */
    background-size: cover;
    margin-bottom: 7px;
    margin-right: 3px;
}

.state-available {
    background-color: #d9b674;
    position: absolute;
    height: 17px;
    width: 65px;
    top: 8px;
    left: 0px;
}

.state-sold-out {
    /*左上角提示栏已售空样式*/
    background-color: gray;
    position: absolute;
    height: 17px;
    width: 65px;
    top: 9px;
    left: 0px;
}

.state-card-disable {
    /*已售空遮罩层*/
    position: relative;
}

/* 伪元素作为遮罩 */
.state-card-disable::after {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    /* 半透明遮罩 */
    pointer-events: none;
    /* 遮罩不影响交互 */
}

/*金币不足样式*/
.coin-shortage {
    color: red;
    font-size: 13px;
}
</style>