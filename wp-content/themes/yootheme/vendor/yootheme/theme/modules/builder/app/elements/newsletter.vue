<script>

    import Entity from '../components/entity';
    import Element from '../components/element.vue';

    export default {

        title: 'Newsletter',

        element: true,

        mixins: [Entity, Element],

        params: ({element}) => ({

            width: 600,
            tabs: [

                {
                    title: 'Content',
                    fields: {

                        'provider.name': {
                            label: 'Provider',
                            type: 'select',
                            options: {
                                'Mailchimp': 'mailchimp',
                                'Campaign Monitor': 'cmonitor'
                            }
                        },

                        mailchimp: {
                            label: 'Mailchimp',
                            type: 'newsletter-lists',
                            provider: 'mailchimp',
                            show: ({provider}) => provider.name == 'mailchimp'
                        },

                        cmonitor: {
                            label: 'Campaign Monitor',
                            type: 'newsletter-lists',
                            provider: 'cmonitor',
                            show: ({provider}) => provider.name == 'cmonitor'
                        },

                        'provider.after_submit': {
                            label: 'After Submit',
                            description: 'Select whether a message will be shown or the site will be redirected after clicking the subscribe button.',
                            type: 'select',
                            options: {
                                'Show message': 'message',
                                'Redirect': 'redirect'
                            }
                        },

                        'provider.message': {
                            label: 'Message',
                            type: 'textarea',
                            description: 'Message shown to the user after submit.',
                            attrs: {
                                rows: 4,
                                lazy: true
                            },
                            show: ({provider}) => provider.after_submit == 'message'
                        },

                        'provider.redirect': {
                            label: 'Link',
                            type: 'link',
                            filePicker: false,
                            description: 'Link to redirect to after submit.',
                            show: ({provider}) => provider.after_submit == 'redirect'
                        }
                    }
                },

                {
                    title: 'Settings',
                    fields: {

                        _form: {
                            label: 'Form',
                            divider: true,
                            type: 'group',
                            fields: {

                                layout: {
                                    label: 'Layout',
                                    description: 'Define the layout of the form.',
                                    type: 'select',
                                    options: {
                                        'Grid': 'grid',
                                        'Stacked': 'stacked',
                                        'Stacked (Name fields as grid)': 'stacked-name'
                                    }
                                },

                                show_name: {
                                    type: 'checkbox',
                                    text: 'Show name fields'
                                },

                                gutter: {
                                    label: 'Gutter',
                                    description: 'Set the gutter for the form fields.',
                                    type: 'select',
                                    default: '',
                                    options: {
                                        'Small': 'small',
                                        'Medium': 'medium',
                                        'Default': ''
                                    }
                                },

                                form_size: {
                                    label: 'Size',
                                    type: 'select',
                                    default: '',
                                    options: {
                                        'Small': 'small',
                                        'Default': '',
                                        'Large': 'large'
                                    }
                                }
                            }
                        },

                        _labels: {
                            label: 'Labels',
                            divider: true,
                            type: 'group',
                            fields: {

                                label_email: {
                                    label: 'Email',
                                    attrs: {
                                        placeholder: 'Email address'
                                    }
                                },

                                label_button: {
                                    label: 'Button',
                                    attrs: {
                                        placeholder: 'Submit'
                                    }
                                },

                                label_first_name: {
                                    label: 'First name',
                                    attrs: {
                                        placeholder: 'First name'
                                    },
                                    enable: ({show_name}) => show_name
                                },

                                label_last_name: {
                                    label: 'Last name',
                                    attrs: {
                                        placeholder: 'Last name'
                                    },
                                    enable: ({show_name}) => show_name
                                }
                            }
                        },

                        _button: {
                            label: 'Button',
                            divider: true,
                            type: 'group',
                            fields: {

                                button_mode: {
                                    label: 'Mode',
                                    description: 'Select whether a button or a clickable icon inside the email input is shown.',
                                    type: 'select',
                                    options: {
                                        'Button': 'button',
                                        'Icon': 'icon'
                                    }
                                },

                                button_style: {
                                    label: 'Style',
                                    description: 'Set the button style.',
                                    type: 'select',
                                    options: {
                                        'Default': 'default',
                                        'Primary': 'primary',
                                        'Secondary': 'secondary',
                                        'Danger': 'danger',
                                        'Text': 'text'
                                    },
                                    enable: ({button_mode}) => button_mode == 'button'
                                },

                                button_fullwidth: {
                                    type: 'checkbox',
                                    text: 'Full width button',
                                    enable: ({button_mode, layout}) => button_mode == 'button' && layout != 'grid'
                                },

                                button_margin: {
                                    label: 'Extra Margin',
                                    description: 'Add extra margin to the button.',
                                    type: 'select',
                                    default: '',
                                    options: {
                                        'None': '',
                                        'Small': 'small',
                                        'Medium': 'default'
                                    },
                                    enable: ({button_mode, show_name}) => button_mode == 'button' && show_name
                                },

                                button_icon: {
                                    label: 'Icon',
                                    description: 'Click on the pencil to pick an icon from the SVG gallery.',
                                    type: 'icon',
                                    enable: ({button_mode}) => button_mode == 'icon'
                                }
                            }
                        },

                        _general: {
                            label: 'General',
                            type: 'group',
                            fields: {
                                text_align: element.text_align_justify,
                                text_align_breakpoint: element.text_align_breakpoint,
                                text_align_fallback: element.text_align_justify_fallback,
                                maxwidth: element.maxwidth,
                                maxwidth_align: element.maxwidth_align,
                                margin: element.margin,
                                margin_remove_top: element.margin_remove_top,
                                margin_remove_bottom: element.margin_remove_bottom,
                                animation: element.animation,
                                _parallax_button: element._parallax_button,
                                visibility: element.visibility
                            }
                        }
                    }
                },

                {
                    title: 'Advanced',
                    fields: {

                        name: element.name,

                        id: element.id,

                        class: element.cls,

                        css: {
                            label: 'CSS',
                            description: 'Enter your own custom CSS. The following selectors will be prefixed automatically for this element: <code>.el-element</code>, <code>.el-input</code>, <code>.el-button</code>',
                            type: 'editor',
                            editor: 'code',
                            mode: 'css',
                            attrs: {
                                debounce: 500
                            }
                        }
                    }
                }
            ]
        }),

        data: () => ({
            props: {
                layout: 'grid',
                show_name: true,
                label_first_name: 'First name',
                label_last_name: 'Last name',
                label_email: 'Email address',
                label_button: 'Subscribe',
                provider: {
                    name: 'mailchimp',
                    after_submit: 'message',
                    message: 'You\'ve been subscribed successfully.',
                    redirect: ''
                },
                mailchimp: {
                    client_id: '',
                    list_id: ''
                },
                cmonitor: {
                    client_id: '',
                    list_id: ''
                },
                button_mode: 'button',
                button_style: 'default',
                button_icon: 'mail'
            }
        })

    }

</script>
