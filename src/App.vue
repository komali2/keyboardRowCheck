<template>
  <main>
    <header>
      <h1>
        Is your text on a single row?
        <small>
          Insert it below to find out!
        </small>
      </h1>
    </header>
    <section
      :class="{
        showValid: userInput.length,
        isValid: isValid(userInput),
        isNotValid: !isValid(userInput)
      }"
    >
      <input v-model="userInput" />
      <div v-if="isValid(userInput)">
        It's valid!
      </div>
      <div v-if="!isValid(userInput)">
        It's not valid :(
      </div>
      <select v-model="userSelectedLayout">
        <option disabled value="">Please select keyboard layout</option>
        <option value="usstandard">US Standard QWERTY</option>
        <option value="dvorakus">Dvorak Simplified (US)</option>
      </select>
    </section>
  </main>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      userInput: '',
      userSelectedLayout: '',
      layouts: {
        usstandard: [
          [
            'A',
            'S',
            'D',
            'F',
            'G',
            'H',
            'J',
            'K',
            'L'],
          [
            'Q',
            'W',
            'E',
            'R',
            'T',
            'Y',
            'U',
            'I',
            'O',
            'P',
          ], [
            'Z',
            'X',
            'C',
            'V',
            'N',
            'B',
            'N',
            'M',
          ],
        ],
        dvorakus: [
          [
            'P',
            'Y',
            'F',
            'G',
            'C',
            'R',
            'L',
          ], [
            'A',
            'O',
            'E',
            'U',
            'I',
            'D',
            'H',
            'T',
            'N',
            'S',
          ], [
            'Q',
            'J',
            'K',
            'X',
            'B',
            'M',
            'W',
            'V',
            'Z',
          ],
        ],
      },
    };
  },
  methods: {
    isValid(input) {
      if (!input.length || !this.userSelectedLayout.length) {
        return false;
      }
      // Determine which row this string may be on
      let keyRow = null;
      const layout = this.layouts[this.userSelectedLayout];

      // eslint-disable-next-line
      layout.forEach((row)=>{
        if (row.includes(input[0].toUpperCase())) {
          keyRow = row;
        }
      });
      if (!keyRow) return false;

      // eslint-disable-next-line
      for (let j = 0; j < input.length; j++) {
        if (!keyRow.includes(input[j].toUpperCase())) {
          return false;
        }
      }
      return true;
    },
  },
};

</script>

<style>
body {
  background-color: #f4f4f4;
  font-family: helvetica neue,helvetica,sans-serif;
  line-height: 1.4;
}
main {
  margin-left: auto;
  margin-right: auto;
  max-width: 34em;
}
header {
  font-size: 2em;
  line-height: 1.1;
}

h1 small, h2 small, h3 small, h4 small {
  display: block;
}

h3 small {
  font-weight: normal;
}

main section {
  border: 1px solid;
  border-color: black;
  padding: 10px;
  margin-bottom: 10px;
  display: flex;
  flex-flow: column;
  justify-content: center;
  align-items: center;
  transition-property: border-color;
  transition-duration: 1s;
}
main section div {
   margin: 8px 0px;
 }
main section input {
   margin: 8px 0px;
 }
 main section select {
   margin: 8px 0px;
 }

 section.showValid.isValid {
   border: 3px solid;
   border-color: green;
 }
 section.showValid.isNotValid {
   border: 3px solid;
   border-color: red;
 }

main small {
  font-weight: normal
}

@media only screen {

 } /* Define mobile styles */

@media only screen and (min-width: 40.063em) {
 } /* min-width 641px, medium screens */

@media only screen and (min-width: 64.063em) {
 } /* min-width 1025px, large screens */

@media only screen and (min-width: 90.063em) { } /* min-width 1441px, xlarge screens */

@media only screen and (min-width: 120.063em) { } /* min-width 1921px, xxlarge screens */

</style>
