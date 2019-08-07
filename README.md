## progress-comp

**progress-comp** is a simple progress bar web component (Vue.js >= 2.5) with styling and labelling options.  

**progress-comp** can be installed via with the included `package.json` file for a local installation via the [npm install](https://docs.npmjs.com/cli/install.html "npm install") command.  **progress-comp** depends on the [vue.js](https://vuejs.org/ "Vue.js") framework.  A demo folder is provided that used [Parcel](https://parceljs.org/) together with its associated `package.json` file to bundle together  **progress-comp** along with its [vue.js](https://vuejs.org/ "Vue.js") dependency for a simple application.  Further details are provided below for running the demo.

## Props

A prop in Vue.js is a custom attribute for passing information from a parent component hosting **progress-comp** instance(s) to an **progress-comp** as a child component. 

**progress-comp** has the following props for a parent to bind and send information to:

`heading` -- a heading for the component that can be positioned above, below, or to the left of the input box (string, default: `null`)

`percent` -- a number that sets the current percent on the progress bar (number, default: null)

`layout` -- determines the position of the above `heading`as 'top', 'bottom', or 'left' (string, default: 'left')

`css_variables` -- defines the css variables for **progress-comp** (object, default: null)

## Styling

The **css_variables** prop is a javascript object that contains any combination of css variable names as keys and associated values.  The following list are the css variable names along with their default values for a quick styling of **progress-comp**:

```
  {
      progress_comp_font_family: 'Verdana,serif',
      progress_comp_font_size: '1rem',

      progress_comp_heading_color: 'black',
      progress_comp_heading_font_weight: 'bold',

      progress_comp_track_height: '.8rem',
      progress_comp_track_width: '25rem',
      progress_comp_track_background: '#555',
      progress_comp_track_border: '1px solid black'

      progress_comp_bar_background: 'linear-gradient(to bottom, #b4e391 0%,#61c419 50%,#b4e391 100%)'
  }
```

As an example you could bind from the parent the following object to the `css_variables` prop for setting the heading color and the track border of **progress-comp**:

```
{progress_comp_heading_color: 'white', progress_comp_track_border: '1px solid white'}
```

Note that multiple **progress-comp** children of the parent can each be bound to a unique set of `css_variable` prop objects. To enforce the same styling across all **progress-comp** children, simply  bind just one `css_variable` prop object to all the **progress-comp** children.

## Events

There are no events

## Demonstration

One demonstration of **progress-comp**  is provided in the folder named `demo/dist` and can be viewed by hosting the `index.html` file.  The demo (templated in the `App.vue` file) displays a labelled progress bar where the parent  continuously emits a 'progress_comp_percent' event for setting the percent from 0 to 100.

As a suggestion, install [http-server](https://www.npmjs.com/package/http-server "http-server") locally/globally via [npm](https://www.npmjs.com/ "npm") then enter the command `http-server`in the **button-comp** `dist` directory.  From a browser enter the url: `localhost:8080/` to view the demo.

Here is some example code for using **progress-comp** taken from the `App.vue` file:

```
      <button v-on:click="start_download">Start Download</button>   
      <progress-comp
      	layout="top"
        :heading="heading"
        :percent="percent"
        :css_variables="css_variables">
      </progress-comp>
```

And here is the supporting data references:

```
  data() {
    return {
      heading: 'Download Progress',
      percent: 0,
      css_variables: {
        progress_comp_heading_color: 'white',
        progress_comp_track_border: '1px solid white'
      }
    }
  },
  methods: {
    start_download: function() {
      let width = 0;
      setInterval(() =>{
        width = width >= 100 ? 0 : width+5;
        this.percent = width;
      },300);
    }
  }
```

