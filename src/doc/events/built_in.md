# Built in events

## Duckvil::Editor::
- ### CloseWidgetEvent
  ```cpp
  struct CloseWidgetEvent
  {
      RuntimeReflection::__duckvil_resource_type_t m_typeHandle;
      void* m_pObject; // Indicates which instance to close

      CloseWidgetEvent(
        const RuntimeReflection::__duckvil_resource_type_t& _typeHandle,
        void* _pObject
      ) :
          m_typeHandle(_typeHandle),
          m_pObject(_pObject)
      {

      }

      template <typename Type>
      CloseWidgetEvent(Type* _pObject) :
          m_pObject(_pObject)
      {
          m_typeHandle = RuntimeReflection::get_type<Type>();
      }
  };
  ```
- ### SpwanWidgetEvent
  ```cpp
  struct SpwanWidgetEvent
  {
      RuntimeReflection::__duckvil_resource_type_t m_typeHandle;
  };
  ```

## Duckvil::
- ### InjectConstructorArgumentEvent
  ```cpp
  struct InjectConstructorArgumentEvent
  {
      struct Info
      {
          RuntimeReflection::__duckvil_resource_type_t m_typeHandle;
          RuntimeReflection::__duckvil_resource_constructor_t m_constructorHandle;
          uint32_t m_uiArgumentIndex;
      };

      bool m_bSuccess;
      FunctionArgumentsPusher* m_pFAP;
      InjectConstructorArgumentEvent::Info m_info;
      RuntimeReflection::__argument_t m_argument;

      InjectConstructorArgumentEvent(
        FunctionArgumentsPusher* _pFAP,
        const InjectConstructorArgumentEvent::Info& _info,
        const RuntimeReflection::__argument_t& _argument
      ) :
          m_bSuccess(false),
          m_pFAP(_pFAP),
          m_info(_info),
          m_argument(_argument)
      {

      }
  };
  ```
- ### RequestSystemEvent
  Call to get specified by ```m_typeHandle``` engine system.
  ```cpp
  struct RequestSystemEvent
  {
      RuntimeReflection::__duckvil_resource_type_t m_typeHandle;
      void* m_pRequestedSystem;
  };
  ```

## Duckvil::HotReloader::
- ### AfterCompileEvent
  ```cpp
  struct AfterCompileEvent
  {
      AfterCompileEvent()
      {

      }
  };
  ```
- ### BeforeCompileEvent
  ```cpp
  struct BeforeCompileEvent
  {
      BeforeCompileEvent()
      {

      }
  };
  ```
- ### InternalSwapEvent
  Called **internally** after successful recording new types.
  The ```m_fnSwap``` function pointer should contain logic for search by ```_newTypes``` and swap objects.
  By default, the ```m_fnSwap``` is set to ```Duckvil::RuntimeCompilerSystem::Swap``` function.
  ```cpp
  struct InternalSwapEvent
  {
      Memory::Vector<RuntimeCompilerSystem::hot_object>* m_pHotObjects;
      duckvil_recorderd_types m_recordedTypes;

      void (*m_fnSwap)(
        Memory::Vector<RuntimeCompilerSystem::hot_object>* _pCurrentHotObjects,
        duckvil_recorderd_types& _newTypes
      );
  };
  ```
- ### SwapEvent
  Called **after each** object serialization and deserialization. Useful for catching changes in classes and re-registering systems.
  ```cpp
  struct SwapEvent
  {
      void* m_pOldObject; // Old object
      HotReloader::ITrackKeeper* m_pTrackKeeper; // Brand new object
      Utils::string m_sModuleName; // Filename of the module that contains this type
  };
  ```