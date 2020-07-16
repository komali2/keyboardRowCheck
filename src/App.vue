<template>
  <div>
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
  </div>
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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
