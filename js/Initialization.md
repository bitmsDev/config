# Class: Initialization 

> Configuration 

```js
/**
 *  Run class
 */
const init = new Initialization();

/**
 * All configuration parameters
 */
const configuration = {
    className : {
        complete: 'on-complete',
        error: 'on-error',
        focus: 'on-focus',
        selected: 'on-selected'
    },
    pattern: {
        phone: '7(000)000-00-00'
    }
};

/**
 * Set new configuration in class
 */
init.setConfig(configuration);
```

### className

**className.complete** - this  