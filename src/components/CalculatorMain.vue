<template>
        <div class="c-CalculatorMain-box">
                <div class="c-CalculatorMain-box__screen">
                        <div class="c-CalculatorMain-box__screen__small">
                                {{ first_number }} {{ operator }}
                        </div>
                        {{current_value}}
                </div>
                <div class="c-CalculatorMain-box__buttons">
                        <div class="c-CalculatorMain-box__buttons__row">
                                <button class="c-CalculatorMain-box__buttons__button" @click="handleNumberInput('1')">1</button>
                                <button class="c-CalculatorMain-box__buttons__button" @click="handleNumberInput('2')">2</button>
                                <button class="c-CalculatorMain-box__buttons__button" @click="handleNumberInput('3')">3</button>
                                <button class="c-CalculatorMain-box__buttons__button c-CalculatorMain-box__buttons__button--operator" @click="handleOperatorInput('+')">+</button>
                        </div>
                        <div class="c-CalculatorMain-box__buttons__row">
                                <button class="c-CalculatorMain-box__buttons__button" @click="handleNumberInput('4')">4</button>
                                <button class="c-CalculatorMain-box__buttons__button" @click="handleNumberInput('5')">5</button>
                                <button class="c-CalculatorMain-box__buttons__button" @click="handleNumberInput('6')">6</button>
                                <button class="c-CalculatorMain-box__buttons__button c-CalculatorMain-box__buttons__button--operator" @click="handleOperatorInput('-')">-</button>
                        </div>
                        <div class="c-CalculatorMain-box__buttons__row">
                                <button class="c-CalculatorMain-box__buttons__button" @click="handleNumberInput('7')">7</button>
                                <button class="c-CalculatorMain-box__buttons__button" @click="handleNumberInput('8')">8</button>
                                <button class="c-CalculatorMain-box__buttons__button" @click="handleNumberInput('9')">9</button>
                                <button class="c-CalculatorMain-box__buttons__button c-CalculatorMain-box__buttons__button--operator" @click="handleOperatorInput('*')">*</button>
                        </div>
                        <div class="c-CalculatorMain-box__buttons__row">
                                <button class="c-CalculatorMain-box__buttons__button c-CalculatorMain-box__buttons__button--clear" @click="handleActionInput('C')">C</button>
                                <button class="c-CalculatorMain-box__buttons__button" @click="handleNumberInput('0')">0</button>
                                <button class="c-CalculatorMain-box__buttons__button " @click="handleActionInput('=')">=</button>
                                <button class="c-CalculatorMain-box__buttons__button c-CalculatorMain-box__buttons__button--operator" @click="handleOperatorInput('/')">/</button>
                        </div>
                </div>
        </div>
</template>
 
<script>
        export default {
                data() {
                        return {
                                current_value: 0,
                                first_number: null,
                                operator: '',
                                afterResult: false
                        }
                },
                methods: {
                        handleNumberInput(number){
                                if(this.current_value == 0 || this.afterResult){
                                        this.current_value = number;
                                        this.afterResult = false;
                                        return;
                                }
                                if(this.current_value.length > 10){
                                        window.alert("Your number is to big!");
                                        return;
                                }
                                this.current_value += number;
                               

                        },
                        handleOperatorInput(operator){
                                this.current_value != 0 ? this.first_number = parseFloat(this.current_value): 0;
                                this.current_value = 0;
                                this.operator = operator

                        },
                        handleActionInput(action) {
                                switch (action) {
                                        case 'C':
                                                this.first_number = null;
                                                this.current_value = 0;
                                                this.operator = '';
                                                break;
                                        case '=':
                                                this.handleOperation();
                                                this.afterResult = true;
                                                break;
                                
                                        default:
                                                break;
                                }
                        },
                        handleOperation(){
                                
                                if (this.first_number == null || this.current_value == 0){
                                        return;
                                }
                                this.current_value = parseFloat(this.current_value)
                                this.first_number = parseFloat(this.first_number)
                                switch (this.operator) {
                                        case '+':
                                                this.current_value += this.first_number;
                                                this.first_number = null;
                                                this.operator = ''
                                                break;
                                        case '-':
                                                this.current_value -= this.first_number;
                                                this.first_number = null;
                                                this.operator = ''
                                                break;
                                        case '*':
                                                this.current_value *= this.first_number;
                                                this.first_number = null;
                                                this.operator = ''
                                                break;
                                        case '/':
                                                this.current_value /= this.first_number;
                                                this.current_value *= 1000
                                                this.current_value = Math.round(this.current_value)/1000
                                                this.first_number = null;
                                                this.operator = ''
                                                break;
                                
                                        default:
                                                
                                                break;
                                }
                        }
                }
        }

</script>



<style lang="scss" >
        $dark-blue-bg: #09277977;
        $light-blue-bg: #80808033;
        .c-CalculatorMain-box{
                width: 450px;
                height: 600px;
                padding: 20px;
                border-radius: 20px;
                box-sizing: border-box;
                background-color: $light-blue-bg;
                display: flex;
                flex-direction: column;
                position: relative;
                &__screen{
                        width: 100%;
                        height: 20%;
                        border-radius: 20px;
                        padding: 15px;
                        box-sizing: border-box;
                        background-color: $dark-blue-bg;
                        display: flex;
                        justify-content: end;
                        flex-direction: column;
                        align-items: end;
                        font-size: 3rem;
                        &__small{
                                font-size: 2rem;
                        }

                }
                &__buttons{
                        position: relative;
                        display: flex;
                        flex-direction: column;
                        justify-content: center;
                        align-items: center;
                        height: 80%;
                        gap: 10px;
                        &__row{
                                display: flex;
                                gap: 10px;
                        }
                        &__button{
                                aspect-ratio: 1;
                                width: 95px;
                                border: none;
                                border-radius: 10px;
                                background-color: $dark-blue-bg;
                                font-size: 30px;
                                transition: all 0.2s;
                                &:hover{
                                        border: 5px solid $dark-blue-bg ;
                                        background-color: $light-blue-bg;

                                }
                                &--clear{
                                        background-color: #041e6b9a;
                                }
                                &--operator{
                                        background-color: #041e6b9a;
                                }
                        }


                }
        }

</style>