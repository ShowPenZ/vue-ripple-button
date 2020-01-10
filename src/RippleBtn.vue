
<script>
import ClassName from "classnames";

function debounce(func, delay) {
  let inDebounce = "";
  inDebounce = undefined;

  return () => {
    let args = "";
    let context = "";

    context = this;
    args = arguments;

    clearTimeout(inDebounce);

    return (inDebounce = setTimeout(() => func.apply(context, args), delay));
  };
}

const RippleBtn = {
  name: "RippleBtn",
  props: {
    btnClassName: {
      type: String,
      required: false
    },
    btnStyle: {
      type: Object,
      required: false
    },
    text: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      ripples: null,
      ripple: null,
      rippleContainer: null
    };
  },
  mounted() {
    const that = this;

    that.ripples = document.querySelectorAll("[ripple]");

    that.rippleContainer = document.createElement("div");
    that.rippleContainer.className = "ripple--container";

    that.ripple = that.ripples;
    that.ripple[0].addEventListener("mousedown", that.showRipple);
    that.ripple[0].addEventListener("mouseup", debounce(that.cleanUp, 2000));
    that.ripple[0].rippleContainer = that.rippleContainer;
    that.ripple[0].appendChild(that.rippleContainer);
  },
  methods: {
    showRipple(e) {
      const that = this;

      let pos = null;
      let rippler = "";
      let size = 0;
      let style = "";
      let x = 0;
      let y = 0;

      rippler = document.createElement("span");

      size = that.rippleContainer.offsetWidth;
      pos = that.rippleContainer.getBoundingClientRect();
      x = e.pageX - pos.left - size / 2;
      y = e.pageY - pos.top - size / 2;

      style =
        "top:" +
        y +
        "px; left: " +
        x +
        "px; height: " +
        size +
        "px; width: " +
        size +
        "px;";

      that.rippleContainer.appendChild(rippler);

      return rippler.setAttribute("style", style);
    },
    cleanUp() {
      const that = this;

      while (that.rippleContainer.firstChild) {
        that.rippleContainer.removeChild(that.rippleContainer.firstChild);
      }
    }
  },

  render() {
    const that = this;
    const { btnClassName, btnStyle, text } = that;

    const onClick = () => {
      that.$emit("onclick", true);
    };

    return (
      <button
        class={ClassName("defaultBtn", btnClassName)}
        ripple="ripple"
        style={btnStyle}
        onClick={onClick}
      >
        {text}
      </button>
    );
  }
};

export default RippleBtn;
</script>
<style>
.defaultBtn {
  background-color: #2ecc71;
  color: #fff;
  border: none;
  padding: 20px;
  margin: 10px;
  font-size: 14px;
  outline: 0;
  box-shadow: 0px 2px 4px 0px #000;
  border-radius: 4px;
}

.defaultBtn:active {
  box-shadow: 0px 2px 6px 0px #000;
}

[ripple] {
  position: relative;
  overflow: hidden;
}

[ripple] .ripple--container {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}

[ripple] .ripple--container span {
  transform: scale(0);
  border-radius: 100%;
  position: absolute;
  opacity: 0.75;
  background-color: #fff;
  animation: ripple 1000ms;
}

@-moz-keyframes ripple {
  to {
    opacity: 0;
    transform: scale(2);
  }
}

@-webkit-keyframes ripple {
  to {
    opacity: 0;
    transform: scale(2);
  }
}

@-o-keyframes ripple {
  to {
    opacity: 0;
    transform: scale(2);
  }
}

@keyframes ripple {
  to {
    opacity: 0;
    transform: scale(2);
  }
}
</style>
