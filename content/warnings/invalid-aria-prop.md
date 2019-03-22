---
title: Invalid ARIA Prop Warning
layout: single
permalink: warnings/invalid-aria-prop.html
---

invalid-aria-prop warning នឹងកើតឡើង ប្រសិនបើអ្នក ព្យាយាម render a DOM element ជាមួយ aria-* prop ដែលមិនមាននៅក្នុង Web Accessibility Initiative (WAI) Accessible Rich Internet Application (ARIA) [ពត៌មានលំអិត](https://www.w3.org/TR/wai-aria-1.1/#states_and_properties)។

១. ប្រសិនបើអ្នក មានអារម្មណ៍ ថាអ្នកបានប្រើប្រាស់ valid prop សូមការពិនិត្យមើល ការសរសេរ ដោយប្រុងប្រយ័ត្ន។ `aria-labelledby` និង `aria-activedescendant` តែងតែមានការ សរសេរខុសច្រើន។

២. React មិនទាន់អាចស្គាល់ attribute ដែលអ្នកបានបង្កើត នៅឡើយទេ។ បញ្ហានេះ អាចនឹងមានដំណោះស្រាយ នៅលើ React ជំនាន់ក្រោយ។ ប៉ុន្តែ សព្វថ្ងៃនេះ React បានធ្វើការដករាល់ attributes ណាដែលមិនស្គាល់ចេញ ដូចនេះការប្រកាស attributes ទាំអស់នៅក្នុង React app នឹងមិនត្រូវបាន rendered នោះទេ។