.. _dev-entities-resolving-orm-query-hints:

Resolving ORM Query Hints
=========================

The |Query Hint Resolver| service has been introduced to make the building of a configuration based queries (like grids, API, etc) easier and more flexible.

To map a hint to a custom tree walker you can use DI container configuration, for example:

.. code-block:: yaml

    oro_security.query_hint.filter_by_current_user:
        public: false
        abstract: true
        tags:
            -
                name: oro_entity.query_hint
                hint: oro_security.filter_by_current_user
                alias: HINT_FILTER_BY_CURRENT_USER
                tree_walker: Oro\Bundle\SecurityBundle\ORM\Walker\CurrentUserWalker
                walker_hint_provider: oro_security.walker_hint_provider.current_user

Please pay attention on `walker_hint_provider` attribute. It is optional and can be used to provide a service to be used to set additional query hints required to work the walker specified in the attribute `tree_walker`. This service must implement |QueryWalkerHintProviderInterface| and must be registered in DI container, for example:

.. code-block:: yaml

    oro_security.walker_hint_provider.current_user:
        public: false
        class: Oro\Bundle\SecurityBundle\ORM\Walker\CurrentUserWalkerHintProvider
        arguments:
             - '@security.token_storage'

To map a hint to a custom output walker use the attribute `output_walker` instead of `tree_walker` in DI container configuration, for example:

.. code-block:: yaml

    oro_translation.query_hint.translatable:
        public: false
        abstract: true
        tags:
            -
                name: oro_entity.query_hint
                hint: oro_translation.translatable
                alias: HINT_TRANSLATABLE
                output_walker: Oro\Component\DoctrineUtils\ORM\Walker\TranslatableSqlWalker

The following example shows how hints can be used in YAML configuration files:

.. code-block:: yaml

    datagrids:
        my-email-origins-grid:
            source:
                type: orm
                query:
                    select:
                        - origin
                    from:
                        - { table: Oro\Bundle\EmailBundle\Entity\EmailOrigin, alias: origin }
                hints:
                    - HINT_FILTER_BY_CURRENT_USER


.. include:: /include/include-links-dev.rst
   :start-after: begin
