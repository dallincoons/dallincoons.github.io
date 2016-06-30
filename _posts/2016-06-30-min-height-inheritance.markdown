---
title: CSS - Min height inheritance

---

So you know how when you use something like `height 100%`, it's based on the height value that was explicitly set on a parent element?

Well, it doesn't work when said parent element has a `min-height` attriubute:

    #a {
        background: cyan;
        min-height: 500px;
    }
    
    #b {
        height: 100%;
        background: mistyrose;
    }

I was able to get around this by giving the child element `position: absolute` and giving the parent `position: relative`.

    #a {
        background: cyan;
        min-height: 500px;
        position: relative;
    }
    
    #b {
        height: 100%;
        background: mistyrose;
        position; absolute;
    }