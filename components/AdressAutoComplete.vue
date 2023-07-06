<template>
  <div class="sm:col-span-6 sm:col-start-1">
    <label for="zip-code" class="block text-sm font-medium leading-6"
      >郵便番号</label
    >
    <div class="mt-2">
      <input
        type="text"
        name="zip-code"
        id="zip-code"
        autocomplete="zip-code"
        minlength="7"
        maxlength="7"
        placeholder="1000001"
        required
        class="block w-full rounded-md py-1.5 input input-bordered input-md sm:max-w-xs sm:text-sm sm:leading-6"
        v-model="inputZip"
        @input="getAddress(computedZip)"
      />
    </div>
  </div>

  <div class="sm:col-span-2">
    <label for="region" class="block text-sm font-medium leading-6"
      >都道府県</label
    >
    <div class="mt-2">
      <input
        type="text"
        name="pref"
        id="pref"
        autocomplete="pref"
        required
        readonly
        disabled
        class="block w-full rounded-md py-1.5 input input-bordered input-md sm:text-sm sm:leading-6"
        :value="pref"
      />
    </div>
  </div>

  <div class="sm:col-span-2">
    <label for="city" class="block text-sm font-medium leading-6"
      >市区町村</label
    >
    <div class="mt-2">
      <input
        type="text"
        name="city"
        id="city"
        autocomplete="city"
        readonly
        disabled
        class="block w-full rounded-md py-1.5 input input-bordered input-md sm:text-sm sm:leading-6"
        :value="city"
      />
    </div>
  </div>

  <div class="sm:col-span-2">
    <label for="town" class="block text-sm font-medium leading-6"
      >地名・番名</label
    >
    <div class="mt-2">
      <input
        type="text"
        name="town"
        id="town"
        autocomplete="town"
        required
        class="block w-full rounded-md py-1.5 input input-bordered input-md sm:text-sm sm:leading-6"
        :value="town"
      />
    </div>
  </div>

  <div class="col-span-full">
    <label for="street-address" class="block text-sm font-medium leading-6"
      >建物名</label
    >
    <div class="mt-2">
      <input
        type="text"
        name="street-address"
        id="street-address"
        autocomplete="street-address"
        required
        class="block w-full rounded-md py-1.5 input input-bordered input-md sm:text-sm sm:leading-6"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, CreateComponentPublicInstance } from "vue";

interface AddressAutoCompleteData {
  inputZip: string;
  defaultZip: string;
  pref: string;
  city: string;
  town: string;
}

export default defineComponent({
  name: "AddressAutoComplete",
  data(): AddressAutoCompleteData {
    return {
      inputZip: "",
      defaultZip: "1000000",
      pref: "",
      city: "",
      town: "",
    };
  },
  computed: {
    computedZip(): string {
      return !isNaN(Number(this.inputZip)) && this.inputZip.length === 7
        ? this.inputZip
        : this.defaultZip;
    },
  },
  methods: {
    getAddress(
      this: CreateComponentPublicInstance<AddressAutoCompleteData>,
      z: string
    ): void {
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
    filterZip(d: string): string {
      const buf = ("0000000" + d).slice(-7);
      return isNaN(+buf) ? "1000000" : buf;
    },
  },
});
</script>
