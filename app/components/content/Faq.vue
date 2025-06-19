<script setup>
const slots = useSlots()

// Créer les items pour l'accordéon à partir des slots
const items = ref([])

// Définir les items statiquement pour éviter les problèmes de slots
onMounted(() => {
  const faqItems = []

  // Extraire le contenu des slots de manière simple
  for (let i = 1; i <= 8; i++) {
    const questionSlot = slots[`question${i}`]
    const answerSlot = slots[`answer${i}`]

    if (questionSlot && answerSlot) {
      // Rendu des slots pour récupérer le texte
      const questionEl = document.createElement('div')
      const answerEl = document.createElement('div')

      // Utiliser innerHTML pour récupérer le contenu
      const questionContent = questionSlot()[0]?.children || ''
      const answerContent = answerSlot()[0]?.children || ''

      if (questionContent && answerContent) {
        faqItems.push({
          label: String(questionContent),
          content: String(answerContent)
        })
      }
    }
  }

  items.value = faqItems
})

// Version alternative : définir les items directement
const staticItems = [
  {
    label: "Comment conserver les produits ?",
    content: "Fermé hermétiquement à l'abri de la chaleur."
  },
  {
    label: "Formats et DDM des produits ?",
    content: "Informations détaillées sur les formats et dates de durabilité minimale de nos produits."
  },
  {
    label: "Modalités de livraison ?",
    content: "Les colis pour un même client passeront toujours par le même transporteur. DPD (5 colis inclus) ou STEF (plusieurs tailles de palettes) avec 2 envois par semaine en moyenne (à partir de 6 colis)."
  },
  {
    label: "Modalités de paiement ?",
    content: "1ère commande : payer le solde avant expédition par virement. Tous les paiements se font par virement à 30 jours max pour les commandes récurrentes."
  },
  {
    label: "Modalités de commande revendeurs ?",
    content: "Montant commande - Remise : <1000 euros (tarif général professionnel), 1000 à 2000 euros (-10%), >2000 euros (-25%)"
  },
  {
    label: "Modalité de commande classique ?",
    content: "100 euros Franco, frais de port 10 euros HT"
  },
  {
    label: "Tarifs et coûts de revient",
    content: "Contactez-nous pour obtenir nos tarifs détaillés et informations sur les coûts de revient."
  },
  {
    label: "Où sommes-nous distribués ?",
    content: "CHR, magasins spécialisés, distributeurs (aventurebio…)"
  }
]
</script>

<template>
  <div class="bg-white py-24 sm:py-32">
    <div class="mx-auto max-w-7xl px-6 lg:px-8">
      <div class="mx-auto max-w-2xl text-center mb-16">
        <h1 v-if="$slots.title" class="text-4xl font-bold tracking-tight text-gray-900 sm:text-5xl">
          <slot name="title" />
        </h1>
        <p v-if="$slots.description" class="mt-6 text-lg leading-8 text-gray-600">
          <slot name="description" />
        </p>
      </div>

      <div class="mx-auto max-w-4xl mt-16">
        <UAccordion
            :items="staticItems"
            class="space-y-4 text-gray-600"
        />
      </div>

      <div class="mx-auto max-w-2xl text-center mt-16">
        <p v-if="$slots.contact_text" class="text-lg text-gray-600 mb-6">
          <slot name="contact_text" />
        </p>
        <UButton
            to="/contact"
            size="lg"
            class="bg-[#824E1E] hover:bg-[#6B3E18] text-white font-semibold px-8 py-3 mt-6 rounded-lg shadow-lg hover:shadow-xl transition-all duration-300"
        >
          <slot name="contact_button" v-if="$slots.contact_button" />
          <span v-else>Nous contacter</span>
        </UButton>
      </div>
    </div>
  </div>
</template>