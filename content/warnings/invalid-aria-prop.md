---
title: Invalid ARIA Prop Warning
layout: single
permalink: warnings/invalid-aria-prop.html
---

ការព្រមាន (warning) invalid-aria-prop នឹង fire ប្រសិនបើអ្នកប៉ុនប៉ង render DOM element ជាមួយ aria-* prop ដែលមិនមាននៅក្នុង Web Accessibility Initiative (WAI) Accessible Rich Internet Application (ARIA) [សម្រាប់ពត៌មានលំអិត](https://www.w3.org/TR/wai-aria-1.1/#states_and_properties)។

1. ប្រសិនបើអ្នកមានអារម្មណ៍ថាអ្នកកំពុងប្រើ prop មួយដែល valid សូមពិនិត្យមើលអក្ខរាវិរុទ្ធដោយប្រុងប្រយ័ត្ន។ `aria-labelledby` និង `aria-activedescendant` ជាញឹកញាប់ត្រូវបានប្រកបខុស។

<<<<<<< HEAD
2. React មិនទាន់អាចស្គាល់ attribute ដែលអ្នកបានបញ្ជាក់នៅឡើយទេ។ បញ្ហានេះនឹងទំនងជាមានដំណេះស្រាយនៅជំនាន់ក្រោយរបស់ React។ ទោះជាយ៉ាងណាក៏ដោយបច្ចុប្បន្ននេះ React ដកចេញនូវរាល់ attributes ណាដែលមិនស្គាល់ទាំងអស់ចេញ ដូច្នេះការបញ្ជាក់ពួកវា (attributes) នៅក្នុង React app របស់អ្នកនឹងមិនត្រូវបាន rendered នេាះទេ។
=======
2. If you wrote `aria-role`, you may have meant `role`.

3. Otherwise, if you're on the latest version of React DOM and verified that you're using a valid property name listed in the ARIA specification, please [report a bug](https://github.com/facebook/react/issues/new/choose).
>>>>>>> 822330c3dfa686dbb3424886abce116f20ed20e6
