<template>
    <div class="calculator">
        <div class="display">{{ current || '0' }}</div>
        <div class="nums">
            <div @click='clear' id="clear" >{{ this.current === '' ? `${'AC'}` : `${'C'}` }}</div>
            <div @click='sign' id="sign">+/-</div>
            <div @click='percent' id="percent">&#37; </div>
            <div @click='append("7")' >7</div>
            <div @click='append("8")' >8</div>
            <div @click='append("9")' >9</div>
            <div @click='append("4")' >4</div>
            <div @click='append("5")' >5</div>
            <div @click='append("6")' >6</div>
            <div @click='append("1")' >1</div>
            <div @click='append("2")' >2</div>
            <div @click='append("3")' >3</div>
            <div @click='append("0")' id="zero">0</div>
            <div @click='dot' >.</div>
        </div>

        <div class="ops">
            <div @click='divide' > &#247; </div>
            <div @click='times' > &#215; </div>
            <div @click='minus' >-</div>
            <div @click='add' >+</div>
            <div @click='equal' id="equals">=</div>
        </div>
    </div>

</template>

<script>
export default {
    name: 'CalculatorComp',
    props: {

    },
    data() {
        return {
            previous: null,
            current: '',
            operator: null,
            operatorClicked: false
        }
    },
    methods: {
        clear() {
            this.current = '';
        },
        sign() {
            if (this.operatorClicked === true) {
                this.current = '';
                this.operatorClicked = false;
            }
            if (this.current === '') {
                this.current = `${'-'}${'0'}`;

            } else {
                this.current = this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`;
            }

        },
        percent() {
            if (this.current !== '') this.current = `${parseFloat(this.current) / 100}`
        },
        append(number) {
            if (this.operatorClicked === true) {
                this.current = '';
                this.operatorClicked = false;
            }

            if (number === '0') {
                if (this.current.charAt(0) === "-" && this.current.charAt(1) === "0") {
                    this.current = `${"-"}${number}`;
                } else
                    if (this.current === '0') {
                        this.current = `${number}`;
                    } else {
                        this.current = `${this.current}${number}`;
                    }
            } else
                if (this.current.charAt(0) === "-" && this.current.charAt(1) === "0" && this.current.indexOf('.') === -1) {
                    this.current = `${"-"}${number}`;
                } else
                    if (this.current.charAt(0) === '0' && this.current.indexOf('.') === -1) {
                        this.current = `${number}`;
                    }
                    else {
                        this.current = `${this.current}${number}`;
                    }
        },
        dot() {
            if (this.current === '') {
                this.current = `${'0'}${'.'}`;
            } else if (this.current.indexOf('.') === -1)
                this.current = `${this.current}${'.'}`;
        },
        setPrevious() {
            this.previous = this.current;
            this.operatorClicked = true;
        },
        divide() {
            this.operator = (a, b) => a / b;
            this.setPrevious();
        },
        times() {
            this.operator = (a, b) => a * b;
            this.setPrevious();
        },
        minus() {
            this.operator = (a, b) => a - b;
            this.setPrevious();
        },
        add() {
            this.operator = (a, b) => a + b;
            this.setPrevious();
        },
        equal() {
            if (this.operatorClicked !== true && this.current !== "" && this.previous !== "") {
                this.current = `${this.operator(parseFloat(this.previous), parseFloat(this.current))}`;
                this.previous = null;
            }
        }
    }
}
</script>

<style scoped>
.calculator {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-gap: 0;
    width: 400px;
    margin: 100px auto;
    box-shadow: 0 0 100px 0 black;
    border-radius: 6px;
    border: 1px solid black;
}

.display,
.nums div,
.ops div {
    border: 1px solid darkgray;
    text-align: center;
    box-sizing: border-box;
    background: linear-gradient(to bottom, #ffffff 0%, #e5e5e5 100%);
    color: #191919;
    user-select: none;
    cursor: pointer;
    width: 100px;
    height: 100px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.display {
    grid-column: 1 / 5;
    display: flex;
    justify-content: flex-end;
    padding-right: 20px;
    font-size: 60px;
    background: #31394C;
    color: #fff;
    border: 0px;
    user-select: auto;
    cursor: text;
    font-weight: normal;
    border-radius: 6px 6px 0px 0px;
    border: 1px solid #31394C;
    width: inherit;
    height: 120px;
}
#clear,
#sign,
#percent{
color: #838383;
}
.nums {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-column: 1 / 4;
    grid-row: 2 / 3;
}
.nums div:active {
    background: darkgray;
}
#equals {
    border-radius: 0px 0px 6px 0px;
}

#zero {
    grid-column: 1/3;
    border-radius: 0px 0px 0px 6px;
    width: 200px !important;
}
.ops {
    display: grid;
    grid-template-columns: 1fr;
}

.ops div {
    background: linear-gradient(to bottom, #DF913C 1%, #DF913C 100%);
    color: #fff;
}

.ops div:active {
    background: #B0732F;
}






</style>
 