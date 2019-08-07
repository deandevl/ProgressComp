<template>
  <div class="progressComp">
    <div :class="compute_container_class()">
      <div class="progressComp_headerBox" v-show="heading">{{heading}}</div>
      <div class="progressComp_trackBox">
        <div class="progressComp_barBox" :style="bar_style"></div>
      </div>
    </div>
    <div class="progressComp_percentBox">{{computed_percent}}</div>
  </div>
</template>

<script>
  export default {
    name: 'ProgressComp',
    data(){
      return {
        bar_style: 'width: 0;'
      }
    },
    props: {
      heading: {
        type: String,
        default: null
      },
      percent: {
        type: Number,
        default: null
      },
      layout: {
        type: String,
        default: 'left'
      },
      css_variables: {
        type: Object,
        default: () => {
          return null;
        }
      }
    },
    computed: {
      computed_percent: function(){
        let percent_text = '0';
        this.bar_style = 'width: 0';
        if(this.percent !== null){
          this.bar_style = `width: ${this.percent}%;`;
          percent_text = `${this.percent}%`;
        }
        return percent_text;
      }
    },
    methods: {
      compute_container_class: function() {
        if(this.layout === 'left'){
          return 'progressComp_headerBox__left';
        }else if(this.layout === 'top'){
          return 'progressComp_headerBox__top';
        }else if(this.layout === 'below'){
          return 'progressComp_headerBox__below';
        }
      }
    },
    mounted(){
      if(this.css_variables !== null){
        for(let key of Object.keys(this.css_variables)){
          this.$el.style.setProperty(`--${key}`, this.css_variables[key]);
        }
      }
    }
  }
</script>

<style lang="less">
  :root {
    --progress_comp_font_family: Verdana,serif;
    --progress_comp_font_size: 1rem;

    --progress_comp_heading_color: black;
    --progress_comp_heading_font_weight: bold;

    --progress_comp_track_height: .8rem;
    --progress_comp_track_width: 25rem;
    --progress_comp_track_background: #555;
    --progress_comp_track_border: 1px solid black;

    --progress_comp_bar_background: linear-gradient(to bottom, #b4e391 0%,#61c419 50%,#b4e391 100%);
  }

  .progressComp {
    display: flex;
    flex-direction: row;
    font-family: var(--progress_comp_font_family);
    font-size: var(--progress_comp_font_size);
    align-items: center;

    &_headerBox {
      color: var(--progress_comp_heading_color);
      font-weight: var(--progress_comp_heading_font_weight);
      margin: .4rem;
    }

    &_headerBox__top {
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    &_headerBox__below {
      display: flex;
      flex-direction: column-reverse;
      align-items: center;
    }
    &_headerBox__left {
      display: flex;
      flex-direction: row;
    }

    &_trackBox {
      height: var(--progress_comp_track_height);
      width: var(--progress_comp_track_width);
      background: var(--progress_comp_track_background);
      border: var(--progress_comp_track_border);
      border-radius: 25px;
      box-shadow: inset 0 -1px 1px rgba(255,255,255,0.3);
    }

    &_barBox {
      background: var(--progress_comp_bar_background);
      height: var(--progress_comp_track_height);
      border-top-right-radius: 8px;
      border-bottom-right-radius: 8px;
      border-top-left-radius: 20px;
      border-bottom-left-radius: 20px;
      box-shadow:
          inset 0 2px 9px  rgba(255,255,255,0.3),
          inset 0 -2px 6px rgba(0,0,0,0.4);
    }

    &_percentBox {
      align-self: flex-end;
      margin-left: .5rem;
      color: var(--progress_comp_heading_color);
    }
  }
</style>