<template>
  <div>
    <label for="zip-code">郵便番号</label>
    <div>
      <input
        type="text"
        name="zip-code"
        id="zip-code"
        autocomplete="zip-code"
        minlength="7"
        maxlength="7"
        placeholder="1000001"
        required
        v-model="inputZip"
        @input="getAddress(computedZip)"
      />
    </div>
  </div>

  <hr />

  <div>
    <label for="region">都道府県</label>
    <div>
      <input
        type="text"
        name="pref"
        id="pref"
        autocomplete="pref"
        required
        readonly
        disabled
        :value="pref"
      />
    </div>
  </div>

  <hr />

  <div>
    <label for="city">市区町村</label>
    <div>
      <input
        type="text"
        name="city"
        id="city"
        autocomplete="city"
        readonly
        disabled
        :value="city"
      />
    </div>
  </div>

  <hr />

  <div>
    <label for="town">地名・番名</label>
    <div>
      <input
        type="text"
        name="town"
        id="town"
        autocomplete="town"
        required
        :value="town"
      />
    </div>
  </div>

  <hr />

  <div>
    <label for="street-address">建物名</label>
    <div>
      <input
        type="text"
        name="street-address"
        id="street-address"
        autocomplete="street-address"
        required
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "AdressAutoComplete",
  data() {
    return {
      inputZip: "",
      defaultZip: "1000000",
      pref: "",
      city: "",
      town: "",
    };
  },
  computed: {
    computedZip() {
      return !isNaN(Number(this.inputZip)) && this.inputZip.length === 7
        ? this.inputZip
        : this.defaultZip;
    },
  },
  methods: {
    getAddress(z: string) {
      fetch(`https://api.zipaddress.net/?zipcode=${z}`)
        .then((res) => res.json())
        .then((data) => {
          this.pref = data.code === 200 ? data.data.pref : data.message;
          this.city = data.code === 200 ? data.data.city : data.message;
          this.town = data.code === 200 ? data.data.town : data.message;
        });
    },
  },
  filters: {
    filterZip(d: string) {
      const buf = ("0000000" + d).slice(-7);
      return isNaN(+buf) ? "1000000" : buf;
    },
  },
});
</script>
