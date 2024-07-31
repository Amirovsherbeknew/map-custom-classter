<template>
  <div>
    <div v-for="(item, index) in data" :key="index" class="editor-box">
      <div class="toolbar">
        <button @click="toggleStyle('bold', index)"><b>B</b></button>
        <button @click="toggleStyle('italic', index)"><i>I</i></button>
        <button @click="toggleStyle('underline', index)"><u>U</u></button>
        <select v-model="fontSize[index]" @change="applyFontSize(index)">
          <option value="8pt">8pt</option>
          <option value="10pt">10pt</option>
          <option value="12pt">12pt</option>
          <option value="14pt">14pt</option>
          <option value="18pt">18pt</option>
          <option value="24pt">24pt</option>
          <option value="36pt">36pt</option>
        </select>
        <input type="color" @change="applyColor($event)">
      </div>
      <div contenteditable="true" :id="`editor-${index}`" @mouseup="selectText(index)" @input="handleChange(index, $event)" v-html="item"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'NuxtTutorial',
  data() {
    return {
      data: ['<b>hiv</b> <i>sdfsdfsdf</i> dssfsdf <br/>'],
      fontSize: []
    };
  },
  methods: {
    selectText(index) {
      const selection = window.getSelection();
      if (selection) {
        console.log(`Selected text in editor-${index}:`, selection.toString());
      }
    },
    handleChange(index, event) {
      console.log(`Current content in editor-${index}:`, event.target.innerHTML);
      const element = document.getElementById(`editor-${index}`)
      if (element.clientHeight > 420) {
        this.data = this.data.push(event.target)
      }
      else  {
        this.data[index] = event.target;
      }
    },
    toggleStyle(style, index) {
      const selection = window.getSelection();
      if (!selection.rangeCount) return;

      const range = selection.getRangeAt(0);
      const parent = range.commonAncestorContainer.parentElement;

      if (parent && parent.style[style]) {
        parent.style[style] = '';
      } else {
        this.applyStyle(style, index);
      }
    },
    applyStyle(style, index) {
      const selection = window.getSelection();
      if (!selection.rangeCount) return;

      const range = selection.getRangeAt(0);
      const selectedText = range.extractContents();
      
      let span = document.createElement('span');
      if (style === 'bold') span.style.fontWeight = 'bold';
      if (style === 'italic') span.style.fontStyle = 'italic';
      if (style === 'underline') span.style.textDecoration = 'underline';
      
      span.appendChild(selectedText);
      range.insertNode(span);
      
      this.handleChange(index, { target: document.getElementById(`editor-${index}`) });
    },
    applyFontSize(index) {
      const selection = window.getSelection();
      if (!selection.rangeCount) return;

      const range = selection.getRangeAt(0);
      const selectedText = range.extractContents();
      
      const span = document.createElement('span');
      span.style.fontSize = this.fontSize[index];
      span.appendChild(selectedText);
      
      range.insertNode(span);
      
      this.handleChange(index, { target: document.getElementById(`editor-${index}`) });
    },
    applyColor(event) {
      const color = event.target.value;
      document.execCommand('foreColor', false, color);
    }
  }
};
</script>

<style>
.editor-box {
  width: 500px;
  height: 600px;
  display: block;
  padding: 6px 8px;
  box-shadow: 4px 4px 8px #ccc;
  border: 1px solid #ddd;
  margin-top: 10px;
  background: #fff;
}
.toolbar {
  margin-bottom: 10px;
}
.toolbar button {
  margin-right: 5px;
  padding: 5px 10px;
  border: 1px solid 
}
</style>