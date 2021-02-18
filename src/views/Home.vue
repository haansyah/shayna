<template>
  <div class="home">
    <HeaderShayna />
    <HeroShayna />
    <WomanShayna />
    <InstaShayna />
    <PartnersShayna />
    <FooterShayna />
  </div>

</template>

<script>
import HeaderShayna from '@/components/HeaderShayna.vue';
import HeroShayna from '@/components/HeroShayna.vue';
import WomanShayna from '@/components/WomanShayna.vue';
import InstaShayna from '@/components/InstaShayna.vue';
import PartnersShayna from '@/components/PartnersShayna.vue';
import FooterShayna from '@/components/FooterShayna.vue';


export default {
  name: 'Home',
  components: {
    HeaderShayna,
    HeroShayna,
    WomanShayna,
    InstaShayna,
    PartnersShayna,
    FooterShayna
  }
}
</script>
